<!-- Content for Post-Implementation Success Emails -->
<div class="email-body">
    <!-- Success Header -->
    <div style="text-align: center; background: linear-gradient(135deg, #2B2B2B 0%, #007FFF 100%); color: #FFFFFF; padding: 24px; border-radius: 8px; margin-bottom: 24px;">
        <h1 style="margin: 0 0 8px 0; font-size: 24px; font-weight: 700;">{{SUCCESS_TITLE}}</h1>
        <p style="margin: 0; font-size: 16px; opacity: 0.9;">{{SUCCESS_SUBTITLE}}</p>
    </div>
    
    <p class="body-text">Hi {{FIRST_NAME}},</p>
    
    {{OPENING_MESSAGE}}
    
    <!-- Results Dashboard -->
    <div style="background-color: #1A1A1A; padding: 24px; border-radius: 8px; margin: 24px 0;">
        <h3 class="heading-medium" style="text-align: center; margin-bottom: 20px; color: #007FFF;">Your Results Dashboard</h3>
        
        <table role="presentation" cellspacing="0" cellpadding="0" border="0" width="100%">
            <tr>
                {{#each RESULTS_METRICS}}
                <td style="text-align: center; padding: 0 12px;">
                    <div style="background-color: #2B2B2B; padding: 16px; border-radius: 6px; border: 1px solid #007FFF;">
                        <p style="margin: 0; font-size: 24px; font-weight: 700; color: #007FFF;">{{value}}</p>
                        <p style="margin: 4px 0 0 0; font-size: 14px; color: #B2B2B2; font-weight: 500;">{{label}}</p>
                    </div>
                </td>
                {{/each}}
            </tr>
        </table>
    </div>
    
    <!-- Quote/Testimonial Section -->
    <div style="background-color: #1A1A1A; color: #FFFFFF; padding: 24px; border-radius: 8px; margin: 24px 0; position: relative; border-left: 4px solid #007FFF;">
        <div style="font-size: 48px; line-height: 1; color: #007FFF; margin-bottom: 12px;">"</div>
        <p style="font-size: 18px; font-style: italic; margin: 0 0 16px 0; line-height: 1.4;">{{TESTIMONIAL_TEXT}}</p>
        <p style="margin: 0; font-size: 14px; font-weight: 600; opacity: 0.8;">— {{CLIENT_NAME}}, {{CLIENT_TITLE}}</p>
    </div>
    
    <!-- Call to Action Section -->
    <div style="background-color: #1A1A1A; border: 2px solid #007FFF; padding: 24px; border-radius: 8px; margin: 24px 0;">
        <h3 class="heading-medium" style="color: #007FFF; margin-bottom: 12px;">{{CTA_TITLE}}</h3>
        <p class="body-text" style="margin-bottom: 20px;">{{CTA_DESCRIPTION}}</p>
        
        <div style="text-align: center;">
            <a href="{{CTA_URL}}" class="cta-button" style="background-color: #007FFF; color: #FFFFFF; padding: 14px 28px; text-decoration: none; border-radius: 6px; font-weight: 600; display: inline-block;">
                {{CTA_TEXT}}
            </a>
        </div>
    </div>
    
    {{CLOSING_MESSAGE}}
    
    <p class="body-text">Best,<br>{{SENDER_NAME}}</p>
</div># Email Design Templates & HTML Code

## Master Email Template Structure

### Brand Color Palette
```css
:root {
  --primary-blue: #1B365D;
  --secondary-orange: #FF6B35;
  --background-gray: #F7F7F7;
  --text-dark: #2C2C2C;
  --text-light: #6B7280;
  --white: #FFFFFF;
  --success-green: #10B981;
  --border-gray: #E5E7EB;
}
```

### Typography System
```css
.email-font-system {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.heading-large { font-size: 24px; font-weight: 700; line-height: 1.2; }
.heading-medium { font-size: 20px; font-weight: 600; line-height: 1.3; }
.heading-small { font-size: 18px; font-weight: 600; line-height: 1.4; }
.body-text { font-size: 16px; font-weight: 400; line-height: 1.6; }
.small-text { font-size: 14px; font-weight: 400; line-height: 1.5; }
.caption-text { font-size: 12px; font-weight: 400; line-height: 1.4; }
```

---

## Base Email Template (HTML)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title>{{EMAIL_TITLE}}</title>
    <!--[if mso]>
    <noscript>
        <xml>
            <o:OfficeDocumentSettings>
                <o:PixelsPerInch>96</o:PixelsPerInch>
            </o:OfficeDocumentSettings>
        </xml>
    </noscript>
    <![endif]-->
    <style type="text/css">
        /* Reset styles */
        body, table, td, p, a, li, blockquote {
            -webkit-text-size-adjust: 100%;
            -ms-text-size-adjust: 100%;
        }
        table, td {
            mso-table-lspace: 0pt;
            mso-table-rspace: 0pt;
        }
        img {
            -ms-interpolation-mode: bicubic;
            border: 0;
            height: auto;
            line-height: 100%;
            outline: none;
            text-decoration: none;
        }

        /* Brand Colors */
        .primary-gray { color: #B2B2B2 !important; }
        .secondary-blue { color: #007FFF !important; }
        .text-white { color: #FFFFFF !important; }
        .text-light { color: #B2B2B2 !important; }
        .bg-dark { background-color: #2B2B2B !important; }
        .bg-darker { background-color: #1A1A1A !important; }

        /* Typography */
        .heading-large {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            font-size: 24px;
            font-weight: 700;
            line-height: 1.2;
            margin: 0 0 16px 0;
            color: #FFFFFF;
        }
        .heading-medium {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            font-size: 20px;
            font-weight: 600;
            line-height: 1.3;
            margin: 0 0 12px 0;
            color: #B2B2B2;
        }
        .body-text {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            font-size: 16px;
            font-weight: 400;
            line-height: 1.6;
            margin: 0 0 16px 0;
            color: #FFFFFF;
        }

        /* Layout */
        .email-container {
            max-width: 600px;
            margin: 0 auto;
            background-color: #2B2B2B;
        }
        .email-header {
            background-color: #1A1A1A;
            padding: 20px;
            text-align: center;
        }
        .email-body {
            padding: 32px 24px;
            background-color: #2B2B2B;
            color: #FFFFFF;
        }
        .email-footer {
            background-color: #1A1A1A;
            padding: 24px;
            text-align: center;
        }

        /* Buttons */
        .cta-button {
            display: inline-block;
            padding: 12px 24px;
            background-color: #007FFF;
            color: #FFFFFF !important;
            text-decoration: none;
            border-radius: 6px;
            font-weight: 600;
            margin: 16px 0;
        }
        .cta-button:hover {
            background-color: #0066CC;
        }

        /* Mobile Responsive */
        @media only screen and (max-width: 480px) {
            .email-container {
                width: 100% !important;
            }
            .email-body {
                padding: 24px 16px !important;
            }
            .heading-large {
                font-size: 20px !important;
            }
            .heading-medium {
                font-size: 18px !important;
            }
        }
    </style>
</head>
<body style="margin: 0; padding: 0; background-color: #1A1A1A;">
    <table role="presentation" cellspacing="0" cellpadding="0" border="0" width="100%">
        <tr>
            <td style="padding: 20px 0;">
                <div class="email-container">
                    <!-- Header -->
                    <div class="email-header">
                        <img src="https://entelech.net/images/logo-white.png" alt="Entelech" width="180" height="auto" style="display: block; margin: 0 auto;">
                        <p style="color: #B2B2B2; margin: 8px 0 0 0; font-size: 14px;">48-Hour Business Transformation</p>
                    </div>

                    <!-- Body Content -->
                    <div class="email-body">
                        {{EMAIL_CONTENT}}
                    </div>

                    <!-- Footer -->
                    <div class="email-footer">
                        <p style="margin: 0 0 8px 0; font-size: 14px; color: #B2B2B2;">
                            <strong style="color: #FFFFFF;">Entelech</strong><br>
                            Richmond, Virginia<br>
                            (804) 972-4550 | sperry@entelech.net
                        </p>
                        <p style="margin: 8px 0 0 0; font-size: 12px; color: #B2B2B2;">
                            <a href="{{UNSUBSCRIBE_URL}}" style="color: #007FFF;">Unsubscribe</a> | 
                            <a href="{{PREFERENCES_URL}}" style="color: #007FFF;">Email Preferences</a>
                        </p>
                    </div>
                </div>
            </td>
        </tr>
    </table>
</body>
</html>
```

---

## Cold Prospect Email Template

```html
<!-- Content for Cold Prospect Emails -->
<div class="email-body">
    <h1 class="heading-large">{{EMAIL_SUBJECT}}</h1>
    
    <p class="body-text">Hi {{FIRST_NAME}},</p>
    
    <div style="background-color: #1A1A1A; padding: 20px; border-left: 4px solid #007FFF; margin: 20px 0; border-radius: 4px;">
        <p class="body-text" style="margin: 0; color: #FFFFFF;">
            <strong>{{KEY_INSIGHT}}</strong>
        </p>
    </div>
    
    {{EMAIL_BODY_CONTENT}}
    
    <!-- Statistics/Results Section -->
    <table role="presentation" cellspacing="0" cellpadding="0" border="0" width="100%" style="margin: 24px 0;">
        <tr>
            <td style="padding: 20px; background-color: #1A1A1A; border-radius: 8px; border: 1px solid #007FFF;">
                <h3 class="heading-medium" style="color: #007FFF;">{{STATS_TITLE}}</h3>
                <ul style="margin: 0; padding-left: 20px; color: #FFFFFF;">
                    <li class="body-text" style="margin-bottom: 8px; color: #FFFFFF;">{{STAT_1}}</li>
                    <li class="body-text" style="margin-bottom: 8px; color: #FFFFFF;">{{STAT_2}}</li>
                    <li class="body-text" style="margin-bottom: 0; color: #FFFFFF;">{{STAT_3}}</li>
                </ul>
            </td>
        </tr>
    </table>
    
    <!-- Call to Action -->
    <div style="text-align: center; margin: 32px 0;">
        <a href="{{CTA_URL}}" class="cta-button">{{CTA_TEXT}}</a>
    </div>
    
    <p class="body-text">Best,<br>Ethan</p>
    
    <p style="font-size: 14px; color: #B2B2B2; margin-top: 24px; padding-top: 16px; border-top: 1px solid #1A1A1A;">
        P.S. {{PS_MESSAGE}}
    </p>
</div>
```

---

## Client Onboarding Email Template

```html
<!-- Content for Client Onboarding Emails -->
<div class="email-body">
    <div style="text-align: center; margin-bottom: 24px;">
        <h1 class="heading-large">{{EMAIL_TITLE}}</h1>
        <p style="font-size: 18px; color: #007FFF; font-weight: 600; margin: 0;">{{SUBTITLE}}</p>
    </div>
    
    <p class="body-text">Hi {{FIRST_NAME}},</p>
    
    {{OPENING_MESSAGE}}
    
    <!-- Progress Indicator -->
    <table role="presentation" cellspacing="0" cellpadding="0" border="0" width="100%" style="margin: 24px 0;">
        <tr>
            <td style="text-align: center;">
                <div style="background-color: #1A1A1A; padding: 16px; border-radius: 8px;">
                    <p style="margin: 0 0 12px 0; font-weight: 600; color: #007FFF;">Implementation Progress</p>
                    <div style="background-color: #2B2B2B; height: 8px; border-radius: 4px; overflow: hidden;">
                        <div style="background-color: #007FFF; height: 100%; width: {{PROGRESS_PERCENTAGE}}%; transition: width 0.3s ease;"></div>
                    </div>
                    <p style="margin: 8px 0 0 0; font-size: 14px; color: #B2B2B2;">{{PROGRESS_TEXT}}</p>
                </div>
            </td>
        </tr>
    </table>
    
    <!-- Checklist Section -->
    <div style="background-color: #1A1A1A; padding: 24px; border-radius: 8px; margin: 24px 0;">
        <h3 class="heading-medium" style="color: #007FFF;">{{CHECKLIST_TITLE}}</h3>
        <table role="presentation" cellspacing="0" cellpadding="0" border="0" width="100%">
            {{#each CHECKLIST_ITEMS}}
            <tr>
                <td style="padding: 8px 0; vertical-align: top; width: 24px;">
                    {{#if completed}}
                    <span style="color: #007FFF; font-size: 18px;">✓</span>
                    {{else}}
                    <span style="color: #B2B2B2; font-size: 18px;">○</span>
                    {{/if}}
                </td>
                <td style="padding: 8px 0 8px 12px;">
                    <p class="body-text" style="margin: 0; {{#if completed}}color: #B2B2B2;{{else}}color: #FFFFFF;{{/if}}">
                        {{text}}
                    </p>
                </td>
            </tr>
            {{/each}}
        </table>
    </div>
    
    <!-- Timeline Section -->
    <h3 class="heading-medium" style="color: #007FFF;">{{TIMELINE_TITLE}}</h3>
    <table role="presentation" cellspacing="0" cellpadding="0" border="0" width="100%" style="margin: 16px 0 24px 0;">
        {{#each TIMELINE_ITEMS}}
        <tr>
            <td style="padding: 12px 0; vertical-align: top; width: 80px;">
                <div style="background-color: {{#if active}}#007FFF{{else}}#1A1A1A{{/if}}; color: #FFFFFF; padding: 6px 12px; border-radius: 4px; text-align: center; font-size: 14px; font-weight: 600;">
                    {{time}}
                </div>
            </td>
            <td style="padding: 12px 0 12px 16px;">
                <p style="margin: 0; font-weight: 600; color: {{#if active}}#007FFF{{else}}#B2B2B2{{/if}};">{{title}}</p>
                <p style="margin: 4px 0 0 0; font-size: 14px; color: #B2B2B2;">{{description}}</p>
            </td>
        </tr>
        {{/each}}
    </table>
    
    <!-- Contact Section -->
    <div style="background-color: #1A1A1A; color: #FFFFFF; padding: 20px; border-radius: 8px; margin: 24px 0; border: 1px solid #007FFF;">
        <h4 style="margin: 0 0 12px 0; font-size: 18px; color: #007FFF;">Questions or Need Help?</h4>
        <p style="margin: 0; font-size: 14px; line-height: 1.5;">
            <strong>Call:</strong> (804) 972-4550<br>
            <strong>Email:</strong> support@entelech.net<br>
            <strong>Response Time:</strong> Within 1 hour during business hours
        </p>
    </div>
    
    {{CLOSING_MESSAGE}}
    
    <p class="body-text">Best,<br>{{SENDER_NAME}}</p>
</div>
```

---

## Success Amplification Email Template

```html
<!-- Content for Post-Implementation Success Emails -->
<div class="email-body">
    <!-- Success Header -->
    <div style="text-align: center; background: linear-gradient(135deg, #1B365D 0%, #FF6B35 100%); color: #FFFFFF; padding: 24px; border-radius: 8px; margin-bottom: 24px;">
        <h1 style="margin: 0 0 8px 0; font-size: 24px; font-weight: 700;">{{SUCCESS_TITLE}}</h1>
        <p style="margin: 0; font-size: 16px; opacity: 0.9;">{{SUCCESS_SUBTITLE}}</p>
    </div>
    
    <p class="body-text text-dark">Hi {{FIRST_NAME}},</p>
    
    {{OPENING_MESSAGE}}
    
    <!-- Results Dashboard -->
    <div style="background-color: #F8FAFC; padding: 24px; border-radius: 8px; margin: 24px 0;">
        <h3 class="heading-medium primary-blue" style="text-align: center; margin-bottom: 20px;">Your Results Dashboard</h3>
        
        <table role="presentation" cellspacing="0" cellpadding="0" border="0" width="100%">
            <tr>
                {{#each RESULTS_METRICS}}
                <td style="text-align: center; padding: 0 12px;">
                    <div style="background-color: #FFFFFF; padding: 16px; border-radius: 6px; border: 1px solid #E5E7EB;">
                        <p style="margin: 0; font-size: 24px; font-weight: 700; color: #FF6B35;">{{value}}</p>
                        <p style="margin: 4px 0 0 0; font-size: 14px; color: #6B7280; font-weight: 500;">{{label}}</p>
                    </div>
                </td>
                {{/each}}
            </tr>
        </table>
    </div>
    
    <!-- Quote/Testimonial Section -->
    <div style="background-color: #1B365D; color: #FFFFFF; padding: 24px; border-radius: 8px; margin: 24px 0; position: relative;">
        <div style="font-size: 48px; line-height: 1; color: #FF6B35; margin-bottom: 12px;">"</div>
        <p style="font-size: 18px; font-style: italic; margin: 0 0 16px 0; line-height: 1.4;">{{TESTIMONIAL_TEXT}}</p>
        <p style="margin: 0; font-size: 14px; font-weight: 600; opacity: 0.8;">— {{CLIENT_NAME}}, {{CLIENT_TITLE}}</p>
    </div>
    
    <!-- Call to Action Section -->
    <div style="background-color: #FFF7ED; border: 2px solid #FF6B35; padding: 24px; border-radius: 8px; margin: 24px 0;">
        <h3 class="heading-medium" style="color: #FF6B35; margin-bottom: 12px;">{{CTA_TITLE}}</h3>
        <p class="body-text text-dark" style="margin-bottom: 20px;">{{CTA_DESCRIPTION}}</p>
        
        <div style="text-align: center;">
            <a href="{{CTA_URL}}" class="cta-button" style="background-color: #FF6B35; color: #FFFFFF; padding: 14px 28px; text-decoration: none; border-radius: 6px; font-weight: 600; display: inline-block;">
                {{CTA_TEXT}}
            </a>
        </div>
    </div>
    
    {{CLOSING_MESSAGE}}
    
    <p class="body-text text-dark">Best,<br>{{SENDER_NAME}}</p>
</div>
```

---

## Mobile-Optimized Components

### Responsive Button Component
```html
<div style="text-align: center; margin: 24px 0;">
    <!--[if mso]>
    <v:roundrect xmlns:v="urn:schemas-microsoft-com:vml" 
                 xmlns:w="urn:schemas-microsoft-com:office:word" 
                 href="{{CTA_URL}}" 
                 style="height:44px;v-text-anchor:middle;width:200px;" 
                 arcsize="14%" 
                 fillcolor="#007FFF">
        <w:anchorlock/>
        <center style="color:#FFFFFF;font-family:Segoe UI,sans-serif;font-size:16px;font-weight:600;">{{CTA_TEXT}}</center>
    </v:roundrect>
    <![endif]-->
    <!--[if !mso]><!-->
    <a href="{{CTA_URL}}" 
       style="background-color: #007FFF; 
              color: #FFFFFF; 
              display: inline-block; 
              font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; 
              font-size: 16px; 
              font-weight: 600; 
              line-height: 44px; 
              text-align: center; 
              text-decoration: none; 
              width: 200px; 
              border-radius: 6px; 
              -webkit-text-size-adjust: none; 
              mso-hide: all;">
        {{CTA_TEXT}}
    </a>
    <!--<![endif]-->
</div>
```

### Social Proof Component
```html
<table role="presentation" cellspacing="0" cellpadding="0" border="0" width="100%" style="margin: 24px 0;">
    <tr>
        <td style="background-color: #1A1A1A; padding: 20px; border-radius: 8px; border-left: 4px solid #007FFF;">
            <table role="presentation" cellspacing="0" cellpadding="0" border="0" width="100%">
                <tr>
                    <td style="width: 60px; vertical-align: top; padding-right: 16px;">
                        <img src="{{CLIENT_AVATAR}}" alt="{{CLIENT_NAME}}" width="48" height="48" style="border-radius: 24px; display: block;">
                    </td>
                    <td style="vertical-align: top;">
                        <p style="margin: 0 0 8px 0; font-size: 16px; font-style: italic; line-height: 1.4; color: #FFFFFF;">"{{TESTIMONIAL_TEXT}}"</p>
                        <p style="margin: 0; font-size: 14px; font-weight: 600; color: #007FFF;">{{CLIENT_NAME}}</p>
                        <p style="margin: 0; font-size: 12px; color: #B2B2B2;">{{CLIENT_TITLE}}, {{CLIENT_COMPANY}}</p>
                    </td>
                </tr>
            </table>
        </td>
    </tr>
</table>
```

### Progress Indicator Component
```html
<div style="margin: 24px 0;">
    <p style="margin: 0 0 8px 0; font-weight: 600; color: #007FFF; text-align: center;">{{PROGRESS_TITLE}}</p>
    <div style="background-color: #1A1A1A; height: 12px; border-radius: 6px; overflow: hidden; margin: 0 auto; max-width: 300px;">
        <div style="background: linear-gradient(90deg, #007FFF 0%, #0066CC 100%); height: 100%; width: {{PROGRESS_PERCENTAGE}}%; border-radius: 6px; transition: width 0.3s ease;"></div>
    </div>
    <p style="margin: 8px 0 0 0; font-size: 14px; color: #B2B2B2; text-align: center;">{{PROGRESS_TEXT}}</p>
</div>
```

---

## Email Testing Checklist

### Cross-Client Testing
- [ ] Gmail (Desktop & Mobile)
- [ ] Outlook 2016/2019/365 (Windows)
- [ ] Outlook Mac
- [ ] Apple Mail (Desktop & iOS)
- [ ] Yahoo Mail
- [ ] Thunderbird

### Mobile Testing
- [ ] iPhone (various screen sizes)
- [ ] Android (various screen sizes)
- [ ] iPad (portrait & landscape)
- [ ] Touch targets minimum 44px
- [ ] Text readable without zooming

### Accessibility Testing
- [ ] Alt text for all images
- [ ] Color contrast ratios meet WCAG AA
- [ ] Screen reader compatibility
- [ ] Keyboard navigation support

### Performance Testing
- [ ] Load time under 3 seconds
- [ ] Image optimization
- [ ] Email size under 100KB
- [ ] Dark mode compatibility

---

## Email Automation Variables

### Personalization Tokens
```javascript
// Basic Personalization
{{FIRST_NAME}} - First name
{{LAST_NAME}} - Last name
{{COMPANY}} - Company name
{{TITLE}} - Job title

// Behavioral Data
{{LAST_EMAIL_OPEN}} - Last email opened date
{{WEBSITE_VISITS}} - Number of website visits
{{CONTENT_DOWNLOADS}} - Downloaded content count
{{LEAD_SCORE}} - Current lead score

// Implementation Data
{{IMPLEMENTATION_DATE}} - Scheduled implementation date
{{PROCESSES_AUTOMATED}} - Number of processes automated
{{TIME_SAVINGS}} - Weekly time savings achieved
{{ROI_PERCENTAGE}} - ROI percentage achieved

// Company Specific
{{INDUSTRY}} - Industry classification
{{REVENUE_RANGE}} - Revenue bracket
{{TEAM_SIZE}} - Number of employees
{{CURRENT_SYSTEMS}} - Existing systems used
```

### Dynamic Content Blocks
```html
<!-- Industry-Specific Content -->
{{#if INDUSTRY_TRANSPORTATION}}
<div class="industry-content">
    <h3>Transportation-Specific Benefits:</h3>
    <ul>
        <li>Route optimization automation</li>
        <li>Driver communication streamlining</li>
        <li>Customer tracking notifications</li>
    </ul>
</div>
{{/if}}

<!-- Lead Score Based Content -->
{{#if LEAD_SCORE_HIGH}}
<div class="high-priority-cta">
    <p>Based on your engagement, you're ready for implementation. Let's schedule your 48-hour transformation.</p>
    <a href="{{PRIORITY_CALENDAR_URL}}" class="cta-button">Schedule Priority Consultation</a>
</div>
{{/if}}

<!-- Behavior-Based Content -->
{{#if DOWNLOADED_ROI_CALCULATOR}}
<div class="roi-follow-up">
    <p>Since you've calculated your automation ROI, here's how we can achieve those results...</p>
</div>
{{/if}}
```

This comprehensive email template system ensures consistent branding, optimal deliverability, and maximum conversion rates across all email communications while maintaining professional design and mobile responsiveness.