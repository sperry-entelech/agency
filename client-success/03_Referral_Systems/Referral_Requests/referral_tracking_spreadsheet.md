```
REFERRAL PIPELINE TRACKER
═══════════════════════════════════════════════════════════════

Columns:
A: Referral_ID (Auto-generated: REF-2025-001)
B: Date_Submitted 
C: Referring_Client
D: Referring_Contact_Name
E: Referring_Contact_Email
F: Prospect_Company
G: Prospect_Contact_Name
H: Prospect_Email
I: Prospect_Phone
J: Industry
K: Annual_Revenue_Estimate
L: Employee_Count
M: Qualification_Score (1-10)
N: Status (Lead/Contacted/Discovery/Proposal/Closed-Won/Closed-Lost)
O: Probability (%)
P: Estimated_Deal_Value
Q: Referral_Credit_Amount
R: Initial_Contact_Date
S: Discovery_Call_Date
T: Proposal_Sent_Date
U: Close_Date
V: Won_Lost_Reason
W: Notes
X: Next_Action
Y: Action_Due_Date
Z: Assigned_CSM

FORMULAS:
- Qualification_Score: =IF(K2>500000,3,IF(K2>200000,2,1))+IF(L2>20,2,IF(L2>5,1,0))+IF(N2="Discovery",2,IF(N2="Contacted",1,0))
- Referral_Credit: =IF(N2="Closed-Won",IF(P2>10000,5000,IF(P2>5000,3500,2500)),0)
- Days_in_Pipeline: =TODAY()-B2

DASHBOARD SUMMARY (Row 1):
Total Referrals: =COUNTA(A:A)-1
This Month: =COUNTIFS(B:B,">="&DATE(YEAR(TODAY()),MONTH(TODAY()),1))
Qualified: =COUNTIFS(M:M,">=7")
In Discovery: =COUNTIFS(N:N,"Discovery")
Closed Won: =COUNTIFS(N:N,"Closed-Won")
Total Revenue: =SUMIFS(P:P,N:N,"Closed-Won")
Total Credits: =SUMIFS(Q:Q,N:N,"Closed-Won")
Conversion Rate: =COUNTIFS(N:N,"Closed-Won")/COUNTA(A:A)-1

SAMPLE DATA ROWS:
REF-2025-001 | 1/15/2025 | ABC Law Firm | John Smith | john@abclaw.com | DEF Consulting | Jane Doe | jane@defconsult.com | 555-1234 | Professional Services | 750000 | 15 | 8 | Discovery | 75% | 7500 | 3500 | 1/16/2025 | 1/22/2025 | | | | Initial discovery scheduled | Follow up post-discovery | 1/25/2025 | Sarah Johnson
```