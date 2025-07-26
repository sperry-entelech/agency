REFERRAL REWARDS & CREDITS TRACKER
═══════════════════════════════════════════════════════════════

PURPOSE: Track Champions program performance, tier advancement, and credit distribution across all referral activities.

Columns:
A: Champion_Name
B: Champion_Company  
C: Champion_Tier (Ambassador/Partner/Leader)
D: Referral_Date
E: Prospect_Company
F: Deal_Value
G: Close_Date
H: Referral_Credit_Earned
I: Credit_Applied_Date
J: Running_Credit_Balance
K: Total_Referrals_Submitted
L: Total_Successful_Conversions
M: Conversion_Rate
N: Total_Credits_Earned
O: Next_Tier_Requirements
P: Tier_Advancement_Progress

DASHBOARD METRICS:
- Total Active Champions: =COUNTA(A:A)-1
- Total Referrals This Month: =COUNTIFS(D:D,">="&DATE(YEAR(TODAY()),MONTH(TODAY()),1))
- Monthly Conversion Rate: =COUNTIFS(G:G,">="&DATE(YEAR(TODAY()),MONTH(TODAY()),1))/COUNTIFS(D:D,">="&DATE(YEAR(TODAY()),MONTH(TODAY()),1))
- Credits Awarded This Month: =SUMIFS(H:H,I:I,">="&DATE(YEAR(TODAY()),MONTH(TODAY()),1))
- Average Deal Size: =AVERAGE(F:F)

AUTOMATED CALCULATIONS:
- Referral Credit: =IF(F2>10000,5000,IF(F2>5000,3500,2500))
- Tier Advancement: =IF(K2>=6,"Transformation Leader",IF(K2>=3,"Innovation Partner","Automation Ambassador"))
- Next Milestone: =IF(O2="Transformation Leader","Achieved",IF(O2="Innovation Partner",6-K2&" more referrals",3-K2&" more referrals"))

SAMPLE DATA:
John Smith | ABC Law Firm | Ambassador | 1/15/2025 | DEF Consulting | 7500 | 2/1/2025 | 3500 | 2/1/2025 | 3500 | 2 | 1 | 50% | 3500 | Innovation Partner | 2 more referrals needed