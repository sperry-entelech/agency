# Technical Setup Procedures

### Overview
This document provides comprehensive, step-by-step procedures for setting up the complete technical infrastructure required for Entelech AI's 48-hour automation implementations. These procedures ensure consistent, reliable, and secure deployment of Azure infrastructure, PostgreSQL databases, and n8n automation platforms.

### Infrastructure Architecture Overview

#### **Technology Stack Components**
- **Cloud Platform**: Microsoft Azure (Primary hosting and infrastructure)
- **Compute**: Azure Virtual Machines (Standard D4s v3 or higher)
- **Database**: PostgreSQL 15+ (Primary data storage and management)
- **Automation Platform**: n8n (Workflow automation and integration)
- **AI Integration**: OpenAI GPT-4/Claude API integration
- **Security**: SSL/TLS encryption, Azure security groups, firewall configuration
- **Monitoring**: Azure Monitor, Application Insights, custom dashboards

#### **Network Architecture Design**
```markdown
Internet Gateway
    ↓
Azure Load Balancer
    ↓
Public Subnet (Web Tier)
    ├── n8n Application Server
    ├── Web Dashboard Interface
    └── SSL Termination
    ↓
Private Subnet (Application Tier)
    ├── API Gateway
    ├── AI Integration Services
    └── Business Logic Processing
    ↓
Private Subnet (Database Tier)
    ├── PostgreSQL Primary
    ├── PostgreSQL Replica (Backup)
    └── Redis Cache
```

### Phase 1: Azure Infrastructure Deployment

#### **Step 1: Azure Resource Group Creation**
**Estimated Time**: 15 minutes
**Prerequisites**: Azure subscription with appropriate permissions

**Procedure:**
```bash
# Login to Azure CLI
az login

# Set subscription (replace with client-specific subscription)
az account set --subscription "subscription-id"

# Create resource group
az group create \
  --name "rg-entelech-client-prod" \
  --location "East US 2" \
  --tags Environment=Production Client=ClientName Project=Automation
```

**Validation Steps:**
- Verify resource group appears in Azure portal
- Confirm location and tags are correctly set
- Validate permissions for resource deployment

#### **Step 2: Virtual Network and Security Configuration**
**Estimated Time**: 20 minutes
**Objective**: Create secure network infrastructure

**Network Creation:**
```bash
# Create virtual network
az network vnet create \
  --resource-group "rg-entelech-client-prod" \
  --name "vnet-entelech-prod" \
  --address-prefix "10.0.0.0/16" \
  --subnet-name "subnet-web" \
  --subnet-prefix "10.0.1.0/24"

# Create application subnet
az network vnet subnet create \
  --resource-group "rg-entelech-client-prod" \
  --vnet-name "vnet-entelech-prod" \
  --name "subnet-app" \
  --address-prefix "10.0.2.0/24"

# Create database subnet
az network vnet subnet create \
  --resource-group "rg-entelech-client-prod" \
  --vnet-name "vnet-entelech-prod" \
  --name "subnet-db" \
  --address-prefix "10.0.3.0/24"
```

**Security Group Configuration:**
```bash
# Create network security group for web tier
az network nsg create \
  --resource-group "rg-entelech-client-prod" \
  --name "nsg-web-tier"

# Allow HTTPS traffic
az network nsg rule create \
  --resource-group "rg-entelech-client-prod" \
  --nsg-name "nsg-web-tier" \
  --name "AllowHTTPS" \
  --protocol "Tcp" \
  --priority 1000 \
  --destination-port-range "443" \
  --access "Allow"

# Allow SSH (temporary for setup)
az network nsg rule create \
  --resource-group "rg-entelech-client-prod" \
  --nsg-name "nsg-web-tier" \
  --name "AllowSSH" \
  --protocol "Tcp" \
  --priority 1100 \
  --destination-port-range "22" \
  --access "Allow"

# Create NSG for database tier
az network nsg create \
  --resource-group "rg-entelech-client-prod" \
  --name "nsg-db-tier"

# Allow PostgreSQL from application subnet only
az network nsg rule create \
  --resource-group "rg-entelech-client-prod" \
  --nsg-name "nsg-db-tier" \
  --name "AllowPostgreSQL" \
  --protocol "Tcp" \
  --priority 1000 \
  --destination-port-range "5432" \
  --source-address-prefix "10.0.2.0/24" \
  --access "Allow"
```

#### **Step 3: Virtual Machine Deployment**
**Estimated Time**: 25 minutes
**Objective**: Deploy and configure primary application server

**VM Creation:**
```bash
# Create public IP
az network public-ip create \
  --resource-group "rg-entelech-client-prod" \
  --name "pip-entelech-app" \
  --allocation-method "Static" \
  --sku "Standard"

# Create network interface
az network nic create \
  --resource-group "rg-entelech-client-prod" \
  --name "nic-entelech-app" \
  --vnet-name "vnet-entelech-prod" \
  --subnet "subnet-app" \
  --public-ip-address "pip-entelech-app" \
  --network-security-group "nsg-web-tier"

# Create virtual machine
az vm create \
  --resource-group "rg-entelech-client-prod" \
  --name "vm-entelech-app" \
  --size "Standard_D4s_v3" \
  --nics "nic-entelech-app" \
  --image "Ubuntu2204" \
  --admin-username "entelech-admin" \
  --ssh-key-values @~/.ssh/id_rsa.pub \
  --os-disk-size-gb 128 \
  --storage-sku "Premium_LRS"
```

**VM Configuration Script:**
```bash
#!/bin/bash
# Initial server setup and hardening

# Update system packages
sudo apt update && sudo apt upgrade -y

# Install essential packages
sudo apt install -y curl wget git vim htop tree unzip nginx certbot python3-certbot-nginx

# Configure firewall
sudo ufw allow OpenSSH
sudo ufw allow 'Nginx Full'
sudo ufw --force enable

# Create application directory structure
sudo mkdir -p /opt/entelech/{n8n,logs,backups,ssl}
sudo chown -R entelech-admin:entelech-admin /opt/entelech

# Set up log rotation
sudo tee /etc/logrotate.d/entelech << EOF
/opt/entelech/logs/*.log {
    daily
    missingok
    rotate 30
    compress
    notifempty
    create 644 entelech-admin entelech-admin
}
EOF
```

#### **Step 4: SSL Certificate Configuration**
**Estimated Time**: 15 minutes
**Objective**: Secure communications with SSL/TLS encryption

**Domain and Certificate Setup:**
```bash
# Configure Nginx for initial setup
sudo tee /etc/nginx/sites-available/entelech << EOF
server {
    listen 80;
    server_name automation.clientdomain.com;
    
    location / {
        return 301 https://\$server_name\$request_uri;
    }
    
    location /.well-known/acme-challenge/ {
        root /var/www/html;
    }
}
EOF

# Enable site
sudo ln -s /etc/nginx/sites-available/entelech /etc/nginx/sites-enabled/
sudo nginx -t && sudo systemctl reload nginx

# Obtain SSL certificate
sudo certbot --nginx -d automation.clientdomain.com --non-interactive --agree-tos --email support@entelech.ai

# Configure automatic renewal
sudo crontab -e
# Add: 0 12 * * * /usr/bin/certbot renew --quiet
```

### Phase 2: Database Infrastructure Setup

#### **Step 5: PostgreSQL Installation and Configuration**
**Estimated Time**: 30 minutes
**Objective**: Deploy optimized PostgreSQL database

**Installation Process:**
```bash
# Install PostgreSQL 15
sudo apt update
sudo apt install -y postgresql-15 postgresql-contrib-15 postgresql-15-pgcrypto

# Start and enable PostgreSQL
sudo systemctl start postgresql
sudo systemctl enable postgresql

# Configure PostgreSQL for production
sudo -u postgres psql << EOF
-- Create database and user for n8n
CREATE DATABASE n8n_production;
CREATE USER n8n_user WITH ENCRYPTED PASSWORD 'secure_random_password_here';
GRANT ALL PRIVILEGES ON DATABASE n8n_production TO n8n_user;

-- Create database for client data
CREATE DATABASE client_data;
CREATE USER client_user WITH ENCRYPTED PASSWORD 'another_secure_password_here';
GRANT ALL PRIVILEGES ON DATABASE client_data TO client_user;

-- Create monitoring user
CREATE USER monitoring_user WITH ENCRYPTED PASSWORD 'monitoring_password_here';
GRANT pg_monitor TO monitoring_user;

-- Exit
\q
EOF
```

**PostgreSQL Optimization Configuration:**
```bash
# Edit PostgreSQL configuration
sudo tee -a /etc/postgresql/15/main/postgresql.conf << EOF
# Performance tuning for D4s_v3 (16GB RAM, 4 vCPUs)
max_connections = 200
shared_buffers = 4GB
effective_cache_size = 12GB
maintenance_work_mem = 1GB
checkpoint_completion_target = 0.9
wal_buffers = 16MB
default_statistics_target = 100
random_page_cost = 1.1
effective_io_concurrency = 200
work_mem = 20MB
min_wal_size = 2GB
max_wal_size = 8GB

# Logging configuration
log_destination = 'stderr'
logging_collector = on
log_directory = '/var/log/postgresql'
log_filename = 'postgresql-%Y-%m-%d_%H%M%S.log'
log_rotation_age = 1d
log_rotation_size = 100MB
log_min_duration_statement = 1000
log_checkpoints = on
log_connections = on
log_disconnections = on
log_lock_waits = on
log_temp_files = 0

# Security settings
ssl = on
ssl_cert_file = '/etc/ssl/certs/ssl-cert-snakeoil.pem'
ssl_key_file = '/etc/ssl/private/ssl-cert-snakeoil.key'
EOF

# Configure client authentication
sudo tee /etc/postgresql/15/main/pg_hba.conf << EOF
# TYPE  DATABASE        USER            ADDRESS                 METHOD
local   all             postgres                                peer
local   all             all                                     md5
host    all             all             127.0.0.1/32            md5
host    all             all             ::1/128                 md5
host    all             all             10.0.0.0/16             md5
EOF

# Restart PostgreSQL
sudo systemctl restart postgresql
```

#### **Step 6: Database Schema Creation**
**Estimated Time**: 20 minutes
**Objective**: Create optimized database schemas

**Core Schema Setup:**
```sql
-- Connect to client_data database
\c client_data;

-- Create core business entities
CREATE TABLE clients (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    industry VARCHAR(100),
    contact_email VARCHAR(255),
    phone VARCHAR(50),
    address TEXT,
    timezone VARCHAR(50) DEFAULT 'UTC',
    status VARCHAR(50) DEFAULT 'active',
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE processes (
    id SERIAL PRIMARY KEY,
    client_id INTEGER REFERENCES clients(id) ON DELETE CASCADE,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    category VARCHAR(100),
    automation_level VARCHAR(50) DEFAULT 'manual',
    priority INTEGER DEFAULT 5,
    estimated_time_hours DECIMAL(5,2),
    actual_time_hours DECIMAL(5,2),
    roi_target DECIMAL(10,2),
    status VARCHAR(50) DEFAULT 'planning',
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE workflows (
    id SERIAL PRIMARY KEY,
    process_id INTEGER REFERENCES processes(id) ON DELETE CASCADE,
    n8n_workflow_id VARCHAR(100) UNIQUE,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    trigger_type VARCHAR(100),
    execution_count INTEGER DEFAULT 0,
    success_count INTEGER DEFAULT 0,
    error_count INTEGER DEFAULT 0,
    avg_execution_time_ms INTEGER,
    last_execution TIMESTAMP,
    status VARCHAR(50) DEFAULT 'active',
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE workflow_executions (
    id SERIAL PRIMARY KEY,
    workflow_id INTEGER REFERENCES workflows(id) ON DELETE CASCADE,
    n8n_execution_id VARCHAR(100),
    status VARCHAR(50),
    start_time TIMESTAMP,
    end_time TIMESTAMP,
    execution_time_ms INTEGER,
    input_data JSONB,
    output_data JSONB,
    error_message TEXT,
    created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE integrations (
    id SERIAL PRIMARY KEY,
    client_id INTEGER REFERENCES clients(id) ON DELETE CASCADE,
    service_name VARCHAR(100) NOT NULL,
    service_type VARCHAR(100),
    api_endpoint VARCHAR(500),
    authentication_type VARCHAR(50),
    credentials_encrypted TEXT,
    rate_limit_per_minute INTEGER DEFAULT 60,
    last_sync TIMESTAMP,
    sync_frequency_minutes INTEGER DEFAULT 60,
    status VARCHAR(50) DEFAULT 'active',
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);

-- Create performance indexes
CREATE INDEX idx_clients_status ON clients(status);
CREATE INDEX idx_processes_client_id ON processes(client_id);
CREATE INDEX idx_processes_status ON processes(status);
CREATE INDEX idx_workflows_process_id ON workflows(process_id);
CREATE INDEX idx_workflows_status ON workflows(status);
CREATE INDEX idx_workflow_executions_workflow_id ON workflow_executions(workflow_id);
CREATE INDEX idx_workflow_executions_created_at ON workflow_executions(created_at);
CREATE INDEX idx_integrations_client_id ON integrations(client_id);
CREATE INDEX idx_integrations_service_name ON integrations(service_name);

-- Create updated_at trigger function
CREATE OR REPLACE FUNCTION update_updated_at_column()
RETURNS TRIGGER AS $$
BEGIN
    NEW.updated_at = NOW();
    RETURN NEW;
END;
$$ language 'plpgsql';

-- Apply updated_at triggers
CREATE TRIGGER update_clients_updated_at BEFORE UPDATE ON clients FOR EACH ROW EXECUTE FUNCTION update_updated_at_column();
CREATE TRIGGER update_processes_updated_at BEFORE UPDATE ON processes FOR EACH ROW EXECUTE FUNCTION update_updated_at_column();
CREATE TRIGGER update_workflows_updated_at BEFORE UPDATE ON workflows FOR EACH ROW EXECUTE FUNCTION update_updated_at_column();
CREATE TRIGGER update_integrations_updated_at BEFORE UPDATE ON integrations FOR EACH ROW EXECUTE FUNCTION update_updated_at_column();
```

#### **Step 7: Database Backup Configuration**
**Estimated Time**: 15 minutes
**Objective**: Implement automated backup strategy

**Backup Script Creation:**
```bash
# Create backup script
sudo tee /opt/entelech/backups/postgres_backup.sh << 'EOF'
#!/bin/bash

# Configuration
BACKUP_DIR="/opt/entelech/backups/postgres"
RETENTION_DAYS=30
DATE=$(date +%Y%m%d_%H%M%S)
DATABASES=("n8n_production" "client_data")

# Create backup directory
mkdir -p $BACKUP_DIR

# Function to backup database
backup_database() {
    local db_name=$1
    local backup_file="$BACKUP_DIR/${db_name}_backup_$DATE.sql.gz"
    
    echo "$(date): Starting backup of $db_name"
    
    sudo -u postgres pg_dump $db_name | gzip > $backup_file
    
    if [ $? -eq 0 ]; then
        echo "$(date): Backup of $db_name completed successfully: $backup_file"
    else
        echo "$(date): ERROR: Backup of $db_name failed"
        exit 1
    fi
}

# Backup each database
for db in "${DATABASES[@]}"; do
    backup_database $db
done

# Clean up old backups
find $BACKUP_DIR -name "*.sql.gz" -mtime +$RETENTION_DAYS -delete

echo "$(date): All database backups completed"
EOF

# Make script executable
sudo chmod +x /opt/entelech/backups/postgres_backup.sh

# Add to crontab for automated backups
(crontab -l 2>/dev/null; echo "0 2 * * * /opt/entelech/backups/postgres_backup.sh >> /opt/entelech/logs/backup.log 2>&1") | crontab -
```

### Phase 3: n8n Platform Deployment

#### **Step 8: n8n Installation and Configuration**
**Estimated Time**: 25 minutes
**Objective**: Deploy and configure n8n automation platform

**Node.js and n8n Installation:**
```bash
# Install Node.js 18 LTS
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs

# Install n8n globally
sudo npm install -g n8n

# Create n8n configuration directory
mkdir -p /opt/entelech/n8n/{workflows,credentials}

# Create n8n environment configuration
tee /opt/entelech/n8n/.env << EOF
# Database configuration
DB_TYPE=postgresdb
DB_POSTGRESDB_HOST=localhost
DB_POSTGRESDB_PORT=5432
DB_POSTGRESDB_DATABASE=n8n_production
DB_POSTGRESDB_USER=n8n_user
DB_POSTGRESDB_PASSWORD=secure_random_password_here

# n8n configuration
N8N_HOST=automation.clientdomain.com
N8N_PORT=5678
N8N_PROTOCOL=https
WEBHOOK_URL=https://automation.clientdomain.com
N8N_BASIC_AUTH_ACTIVE=true
N8N_BASIC_AUTH_USER=admin
N8N_BASIC_AUTH_PASSWORD=admin_password_here

# Security
N8N_JWT_AUTH_ACTIVE=true
N8N_JWT_AUTH_HEADER=authorization
N8N_ENCRYPTION_KEY=encryption_key_32_characters_here

# Execution settings
EXECUTIONS_TIMEOUT=300
EXECUTIONS_TIMEOUT_MAX=3600
EXECUTIONS_DATA_SAVE_ON_ERROR=all
EXECUTIONS_DATA_SAVE_ON_SUCCESS=all
EXECUTIONS_DATA_SAVE_MANUAL_EXECUTIONS=true

# File paths
N8N_USER_FOLDER=/opt/entelech/n8n
WORKFLOWS_FOLDER=/opt/entelech/n8n/workflows
CREDENTIALS_FOLDER=/opt/entelech/n8n/credentials

# Logging
N8N_LOG_LEVEL=info
N8N_LOG_OUTPUT=file
N8N_LOG_FILE_LOCATION=/opt/entelech/logs/n8n.log
EOF
```

#### **Step 9: n8n Service Configuration**
**Estimated Time**: 15 minutes
**Objective**: Configure n8n as system service

**Systemd Service Creation:**
```bash
# Create systemd service file
sudo tee /etc/systemd/system/n8n.service << EOF
[Unit]
Description=n8n workflow automation
After=network.target postgresql.service
Requires=postgresql.service

[Service]
Type=simple
User=entelech-admin
Group=entelech-admin
ExecStart=/usr/bin/n8n start
WorkingDirectory=/opt/entelech/n8n
Environment=NODE_ENV=production
EnvironmentFile=/opt/entelech/n8n/.env
Restart=always
RestartSec=10
StandardOutput=append:/opt/entelech/logs/n8n.log
StandardError=append:/opt/entelech/logs/n8n-error.log

# Security settings
NoNewPrivileges=yes
PrivateTmp=yes
ProtectSystem=strict
ProtectHome=yes
ReadWritePaths=/opt/entelech
CapabilityBoundingSet=CAP_NET_BIND_SERVICE

[Install]
WantedBy=multi-user.target
EOF

# Reload systemd and enable service
sudo systemctl daemon-reload
sudo systemctl enable n8n
sudo systemctl start n8n

# Verify service status
sudo systemctl status n8n
```

#### **Step 10: Nginx Reverse Proxy Configuration**
**Estimated Time**: 20 minutes
**Objective**: Configure secure reverse proxy for n8n

**Nginx Configuration:**
```bash
# Create n8n-specific Nginx configuration
sudo tee /etc/nginx/sites-available/entelech << EOF
# Rate limiting
limit_req_zone \$binary_remote_addr zone=n8n_limit:10m rate=10r/s;

# Upstream n8n server
upstream n8n_backend {
    server 127.0.0.1:5678;
    keepalive 32;
}

server {
    listen 443 ssl http2;
    server_name automation.clientdomain.com;

    # SSL configuration
    ssl_certificate /etc/letsencrypt/live/automation.clientdomain.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/automation.clientdomain.com/privkey.pem;
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers ECDHE-RSA-AES256-GCM-SHA512:DHE-RSA-AES256-GCM-SHA512:ECDHE-RSA-AES256-GCM-SHA384;
    ssl_prefer_server_ciphers off;
    ssl_session_cache shared:SSL:10m;
    ssl_session_timeout 10m;

    # Security headers
    add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
    add_header X-Content-Type-Options "nosniff" always;
    add_header X-Frame-Options "DENY" always;
    add_header X-XSS-Protection "1; mode=block" always;
    add_header Referrer-Policy "no-referrer-when-downgrade" always;

    # Logging
    access_log /var/log/nginx/n8n_access.log;
    error_log /var/log/nginx/n8n_error.log;

    # Rate limiting
    limit_req zone=n8n_limit burst=20 nodelay;

    # Main n8n proxy
    location / {
        proxy_pass http://n8n_backend;
        proxy_http_version 1.1;
        proxy_set_header Upgrade \$http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host \$host;
        proxy_set_header X-Real-IP \$remote_addr;
        proxy_set_header X-Forwarded-For \$proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto \$scheme;
        proxy_cache_bypass \$http_upgrade;
        proxy_read_timeout 300s;
        proxy_connect_timeout 75s;
    }

    # Webhook endpoints (higher rate limits)
    location /webhook/ {
        limit_req zone=n8n_limit burst=100 nodelay;
        proxy_pass http://n8n_backend;
        proxy_http_version 1.1;
        proxy_set_header Host \$host;
        proxy_set_header X-Real-IP \$remote_addr;
        proxy_set_header X-Forwarded-For \$proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto \$scheme;
        proxy_read_timeout 300s;
        proxy_connect_timeout 75s;
    }

    # Health check endpoint
    location /healthz {
        access_log off;
        return 200 "healthy\n";
        add_header Content-Type text/plain;
    }
}

# Redirect HTTP to HTTPS
server {
    listen 80;
    server_name automation.clientdomain.com;
    return 301 https://\$server_name\$request_uri;
}
EOF

# Test and reload Nginx
sudo nginx -t && sudo systemctl reload nginx
```

### Phase 4: Monitoring and Security Hardening

#### **Step 11: Monitoring Setup**
**Estimated Time**: 20 minutes
**Objective**: Implement comprehensive monitoring

**System Monitoring Script:**
```bash
# Create monitoring script
tee /opt/entelech/monitor_system.sh << 'EOF'
#!/bin/bash

LOGFILE="/opt/entelech/logs/monitoring.log"
ALERT_EMAIL="alerts@entelech.ai"

# Function to log with timestamp
log_message() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" >> $LOGFILE
}

# Check system resources
check_resources() {
    CPU_USAGE=$(top -bn1 | grep "Cpu(s)" | awk '{print $2}' | awk -F'%' '{print $1}')
    MEMORY_USAGE=$(free | grep Mem | awk '{printf("%.1f"), $3/$2 * 100.0}')
    DISK_USAGE=$(df -h / | awk 'NR==2{printf "%s", $5}' | sed 's/%//')
    
    log_message "CPU: ${CPU_USAGE}%, Memory: ${MEMORY_USAGE}%, Disk: ${DISK_USAGE}%"
    
    # Alert thresholds
    if (( $(echo "$CPU_USAGE > 80" | bc -l) )); then
        log_message "ALERT: High CPU usage: ${CPU_USAGE}%"
    fi
    
    if (( $(echo "$MEMORY_USAGE > 85" | bc -l) )); then
        log_message "ALERT: High memory usage: ${MEMORY_USAGE}%"
    fi
    
    if [ "$DISK_USAGE" -gt 85 ]; then
        log_message "ALERT: High disk usage: ${DISK_USAGE}%"
    fi
}

# Check services
check_services() {
    services=("postgresql" "nginx" "n8n")
    
    for service in "${services[@]}"; do
        if systemctl is-active --quiet $service; then
            log_message "Service $service is running"
        else
            log_message "ALERT: Service $service is not running"
        fi
    done
}

# Check database connectivity
check_database() {
    if sudo -u postgres psql -c "SELECT 1;" > /dev/null 2>&1; then
        log_message "Database connectivity: OK"
    else
        log_message "ALERT: Database connectivity failed"
    fi
}

# Check n8n API
check_n8n_api() {
    if curl -sf -o /dev/null https://automation.clientdomain.com/healthz; then
        log_message "n8n API health check: OK"
    else
        log_message "ALERT: n8n API health check failed"
    fi
}

# Run all checks
log_message "Starting system monitoring checks"
check_resources
check_services
check_database
check_n8n_api
log_message "Monitoring checks completed"
EOF

# Make script executable
chmod +x /opt/entelech/monitor_system.sh

# Add to crontab (every 5 minutes)
(crontab -l 2>/dev/null; echo "*/5 * * * * /opt/entelech/monitor_system.sh") | crontab -
```

#### **Step 12: Security Hardening**
**Estimated Time**: 25 minutes
**Objective**: Implement security best practices

**System Hardening Script:**
```bash
#!/bin/bash
# Security hardening script

# Disable root SSH login
sudo sed -i 's/#PermitRootLogin yes/PermitRootLogin no/' /etc/ssh/sshd_config
sudo sed -i 's/PermitRootLogin yes/PermitRootLogin no/' /etc/ssh/sshd_config

# Configure SSH security
sudo tee -a /etc/ssh/sshd_config << EOF
# Security configurations
Protocol 2
MaxAuthTries 3
ClientAliveInterval 300
ClientAliveCountMax 2
AllowUsers entelech-admin
PasswordAuthentication no
PubkeyAuthentication yes
X11Forwarding no
PrintMotd no
EOF

# Restart SSH service
sudo systemctl restart sshd

# Install and configure fail2ban
sudo apt install -y fail2ban

# Configure fail2ban for SSH
sudo tee /etc/fail2ban/jail.local << EOF
[DEFAULT]
bantime = 3600
findtime = 600
maxretry = 5
ignoreip = 127.0.0.1/8 10.0.0.0/16

[sshd]
enabled = true
port = ssh
filter = sshd
logpath = /var/log/auth.log
maxretry = 3

[nginx-http-auth]
enabled = true
filter = nginx-http-auth
port = http,https
logpath = /var/log/nginx/error.log

[nginx-limit-req]
enabled = true
filter = nginx-limit-req
port = http,https
logpath = /var/log/nginx/error.log
maxretry = 10
EOF

# Start and enable fail2ban
sudo systemctl start fail2ban
sudo systemctl enable fail2ban

# Configure automatic security updates
sudo apt install -y unattended-upgrades
sudo dpkg-reconfigure -plow unattended-upgrades

# Set up log rotation for application logs
sudo tee /etc/logrotate.d/entelech << EOF
/opt/entelech/logs/*.log {
    daily
    missingok
    rotate 30
    compress
    notifempty
    create 644 entelech-admin entelech-admin
    postrotate
        systemctl reload n8n > /dev/null 2>&1 || true
    endscript
}
EOF

echo "Security hardening completed"
```

### Phase 5: Validation and Testing

#### **Step 13: System Validation**
**Estimated Time**: 30 minutes
**Objective**: Comprehensive system testing

**Validation Test Suite:**
```bash
#!/bin/bash
# Comprehensive system validation

echo "Starting system validation..."

# Test 1: Database connectivity
echo "Testing database connectivity..."
sudo -u postgres psql -c "SELECT version();" -d n8n_production
if [ $? -eq 0 ]; then
    echo "✅ Database connectivity: PASS"
else
    echo "❌ Database connectivity: FAIL"
    exit 1
fi

# Test 2: n8n service status
echo "Testing n8n service..."
if systemctl is-active --quiet n8n; then
    echo "✅ n8n service: PASS"
else
    echo "❌ n8n service: FAIL"
    exit 1
fi

# Test 3: HTTPS certificate validation
echo "Testing SSL certificate..."
if curl -sf -o /dev/null https://automation.clientdomain.com/healthz; then
    echo "✅ HTTPS certificate: PASS"
else
    echo "❌ HTTPS certificate: FAIL"
    exit 1
fi

# Test 4: n8n API response
echo "Testing n8n API..."
response=$(curl -s -o /dev/null -w "%{http_code}" https://automation.clientdomain.com)
if [ "$response" = "200" ] || [ "$response" = "401" ]; then
    echo "✅ n8n API response: PASS"
else
    echo "❌ n8n API response: FAIL (HTTP $response)"
    exit 1
fi

# Test 5: Database performance
echo "Testing database performance..."
start_time=$(date +%s%N)
sudo -u postgres psql -c "SELECT COUNT(*) FROM information_schema.tables;" -d n8n_production > /dev/null
end_time=$(date +%s%N)
duration=$(( (end_time - start_time) / 1000000 ))
if [ "$duration" -lt 1000 ]; then
    echo "✅ Database performance: PASS (${duration}ms)"
else
    echo "⚠️ Database performance: SLOW (${duration}ms)"
fi

# Test 6: Disk space
echo "Testing disk space..."
disk_usage=$(df -h / | awk 'NR==2{printf "%s", $5}' | sed 's/%//')
if [ "$disk_usage" -lt 80 ]; then
    echo "✅ Disk space: PASS (${disk_usage}% used)"
else
    echo "⚠️ Disk space: HIGH (${disk_usage}% used)"
fi

# Test 7: Memory usage
echo "Testing memory usage..."
memory_usage=$(free | grep Mem | awk '{printf("%.0f"), $3/$2 * 100.0}')
if [ "$memory_usage" -lt 70 ]; then
    echo "✅ Memory usage: PASS (${memory_usage}% used)"
else
    echo "⚠️ Memory usage: HIGH (${memory_usage}% used)"
fi

# Test 8: Network connectivity
echo "Testing external network connectivity..."
if ping -c 3 8.8.8.8 > /dev/null 2>&1; then
    echo "✅ External network: PASS"
else
    echo "❌ External network: FAIL"
    exit 1
fi

# Test 9: Backup directory
echo "Testing backup system..."
if [ -d "/opt/entelech/backups" ] && [ -w "/opt/entelech/backups" ]; then
    echo "✅ Backup system: PASS"
else
    echo "❌ Backup system: FAIL"
    exit 1
fi

# Test 10: Log rotation
echo "Testing log rotation..."
if [ -f "/etc/logrotate.d/entelech" ]; then
    echo "✅ Log rotation: PASS"
else
    echo "❌ Log rotation: FAIL"
    exit 1
fi

echo ""
echo "🎉 System validation completed successfully!"
echo "System is ready for production use."
EOF

# Make validation script executable
chmod +x /opt/entelech/validate_system.sh
```

#### **Step 14: Performance Benchmarking**
**Estimated Time**: 20 minutes
**Objective**: Establish performance baselines

**Performance Benchmark Script:**
```bash
#!/bin/bash
# Performance benchmarking script

BENCHMARK_LOG="/opt/entelech/logs/benchmark.log"

echo "Starting performance benchmarking..." | tee -a $BENCHMARK_LOG
echo "Timestamp: $(date)" | tee -a $BENCHMARK_LOG

# Database performance benchmark
echo "=== Database Performance ===" | tee -a $BENCHMARK_LOG
for i in {1..10}; do
    start_time=$(date +%s%N)
    sudo -u postgres psql -c "SELECT COUNT(*) FROM information_schema.columns;" -d n8n_production > /dev/null
    end_time=$(date +%s%N)
    duration=$(( (end_time - start_time) / 1000000 ))
    echo "Query $i: ${duration}ms" | tee -a $BENCHMARK_LOG
done

# Web server response time benchmark
echo "=== Web Server Performance ===" | tee -a $BENCHMARK_LOG
for i in {1..10}; do
    response_time=$(curl -s -w "%{time_total}" -o /dev/null https://automation.clientdomain.com/healthz)
    echo "Request $i: ${response_time}s" | tee -a $BENCHMARK_LOG
done

# System resource baseline
echo "=== System Resources ===" | tee -a $BENCHMARK_LOG
echo "CPU Usage: $(top -bn1 | grep "Cpu(s)" | awk '{print $2}')" | tee -a $BENCHMARK_LOG
echo "Memory Usage: $(free -h | grep Mem | awk '{print $3 "/" $2}')" | tee -a $BENCHMARK_LOG
echo "Disk Usage: $(df -h / | awk 'NR==2{print $3 "/" $2 " (" $5 ")"}')" | tee -a $BENCHMARK_LOG
echo "Load Average: $(uptime | awk -F'load average:' '{print $2}')" | tee -a $BENCHMARK_LOG

echo "Benchmarking completed. Results saved to $BENCHMARK_LOG"
```

### Troubleshooting Guide

#### **Common Issues and Solutions**

**Issue 1: n8n Service Won't Start**
```bash
# Check service status
sudo systemctl status n8n

# Check logs
sudo journalctl -u n8n -f

# Common solutions:
# 1. Check database connectivity
sudo -u postgres psql -c "SELECT 1;" -d n8n_production

# 2. Verify environment file
cat /opt/entelech/n8n/.env

# 3. Check file permissions
sudo chown -R entelech-admin:entelech-admin /opt/entelech/n8n

# 4. Restart service
sudo systemctl restart n8n
```

**Issue 2: Database Connection Errors**
```bash
# Check PostgreSQL status
sudo systemctl status postgresql

# Check database logs
sudo tail -f /var/log/postgresql/postgresql-15-main.log

# Test connection manually
sudo -u postgres psql -h localhost -p 5432 -d n8n_production -U n8n_user

# Reset password if needed
sudo -u postgres psql -c "ALTER USER n8n_user PASSWORD 'new_password';"
```

**Issue 3: SSL Certificate Issues**
```bash
# Check certificate status
sudo certbot certificates

# Renew certificate
sudo certbot renew --dry-run

# Check Nginx configuration
sudo nginx -t

# Reload Nginx
sudo systemctl reload nginx
```

**Issue 4: High Resource Usage**
```bash
# Check top processes
htop

# Check disk usage
du -sh /opt/entelech/*

# Clean up logs if needed
sudo find /opt/entelech/logs -name "*.log" -mtime +7 -delete

# Optimize PostgreSQL if needed
sudo -u postgres psql -c "VACUUM ANALYZE;" -d n8n_production
```

### Security Checklist

#### **Post-Installation Security Validation**
```markdown
☐ SSH Configuration
  - Root login disabled
  - Password authentication disabled
  - SSH key authentication only
  - Custom SSH port (optional)

☐ Firewall Configuration
  - UFW enabled and configured
  - Only necessary ports open (22, 80, 443)
  - Database ports restricted to local network

☐ SSL/TLS Configuration
  - Valid SSL certificate installed
  - Strong cipher suites configured
  - HTTP to HTTPS redirect active
  - Security headers implemented

☐ Database Security
  - Default postgres user secured
  - Application-specific users created
  - Remote access properly restricted
  - Regular backups configured

☐ Application Security
  - n8n basic authentication enabled
  - JWT authentication configured
  - Webhook endpoints secured
  - Rate limiting implemented

☐ System Hardening
  - Fail2ban installed and configured
  - Automatic security updates enabled
  - Log rotation configured
  - Monitoring system active

☐ Backup and Recovery
  - Automated database backups
  - Backup retention policy set
  - Recovery procedures tested
  - Backup storage secured
```

### Maintenance Procedures

#### **Daily Maintenance Tasks**
```bash
#!/bin/bash
# Daily maintenance script

# Check system health
/opt/entelech/monitor_system.sh

# Verify backups
ls -la /opt/entelech/backups/postgres/ | tail -5

# Check disk space
df -h

# Review error logs
sudo tail -50 /opt/entelech/logs/n8n-error.log | grep -i error
```

#### **Weekly Maintenance Tasks**
```bash
#!/bin/bash
# Weekly maintenance script

# Update system packages
sudo apt update && sudo apt list --upgradable

# Analyze database performance
sudo -u postgres psql -c "SELECT schemaname,tablename,attname,n_distinct,correlation FROM pg_stats WHERE tablename IN ('workflows', 'workflow_executions');" -d client_data

# Clean temporary files
sudo find /tmp -type f -atime +7 -delete

# Rotate logs manually if needed
sudo logrotate -f /etc/logrotate.d/entelech

# Check SSL certificate expiration
sudo certbot certificates | grep -A2 -B2 "VALID:"
```

#### **Monthly Maintenance Tasks**
```bash
#!/bin/bash
# Monthly maintenance script

# Full system backup
sudo systemctl stop n8n
/opt/entelech/backups/postgres_backup.sh
sudo tar -czf /opt/entelech/backups/system_backup_$(date +%Y%m%d).tar.gz /opt/entelech
sudo systemctl start n8n

# Security updates
sudo unattended-upgrade -d

# Performance review
/opt/entelech/benchmark_system.sh

# Log analysis
sudo journalctl --since "1 month ago" --until "now" | grep -i error > /opt/entelech/logs/monthly_errors.log

# Update documentation
echo "$(date): Monthly maintenance completed" >> /opt/entelech/logs/maintenance.log
```

This comprehensive technical setup procedure ensures reliable, secure, and performant infrastructure deployment for Entelech AI's 48-hour automation implementations. All procedures are designed for consistency, repeatability, and enterprise-level quality standards.