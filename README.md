# Insurance-Quotation-Motor-Vehicle
🔷 Project Title: Online Insurance Quotation for Motor Vehicle Policy using PEGA
🔶 Introduction
"This project is built using PEGA to automate the motor vehicle insurance quotation process. It allows customers to register, apply for quotes, and track their application status. Agents and staff members can manage these applications, approve or reject them, and generate reports. The goal is to streamline the insurance workflow and reduce manual effort."

🔶 Actors Involved
Agent – Registers customers.
Customer – Applies for quotes.
Staff/Admin – Approves quotes and manages reports.
Quote Officer – Handles manual approvals.
🔶 Modules & Functionalities
✅ 1. Customer Registration
"Agents can register customers by filling in their personal and vehicle details. Once registered, an operator ID is created and login credentials are emailed to the customer. We used a case type with stages like 'Collect Customer Info' and built a section for data entry. An activity handles operator creation and a correspondence rule sends the email. We also implemented session timeout using pxSessionTimer to log out users after 2 minutes of inactivity."

✅ 2. Login Functionality
Customer Login: "Customers log in using credentials received via email. On first login, they update their password. They’re redirected to the CSR portal."
Staff/Admin Login: "Staff log in to the Manager portal. Their access is restricted to data from their registered city."
"Session timeout is consistently handled across all logins using pxSessionTimer."
✅ 3. Dashboards
Customer Dashboard: "Customers can apply for new quotes and view past applications. We reused the OOTB 'My Cases' gadget for history tracking."
Staff/Admin Dashboard: "Staff can view all submitted quotes, generate reports, and export data. Access is restricted by city using access roles and filters."
✅ 4. Quote Application Case Type
"This is the core of the project. It includes four stages:

New Quote Application

Customers enter vehicle details, quote type, IDV, claim count, usage, and payment option.
We used a section for data entry, data transforms for auto-population, and validations for fields like claim count and usage length.
Automatic Eligibility Check

We used a decision tree to check if IDV is ≥ 100000 and claim count ≤ 5.
If the application fails, it’s denied and closed. If it passes, it moves to auto approval.
Automatic Quote Approval

Quotes are auto-approved unless they fail the same eligibility criteria.
Premium is calculated as IDV × 6%, or 5% if claim count ≤ 1.
If auto-approved, the customer sees the premium and accepts terms. If not, the case is routed to the Quote Officer’s workbasket.
We added escalation logic: if pending >3 days, route to manager; if >30 days, auto-reject.
Quote Approval (Manual)

Quote Officers can approve or deny quotes and add comments. We provided a dedicated dashboard view for them.
✅ 5. Email Notifications
"We used correspondence rules to send emails to customers when their quote is submitted, approved, or denied. This keeps them informed throughout the process."

✅ 6. Reporting
"At the end of each business day, a report is generated with all active quote applications. It’s emailed to staff members, filtered by their city. We used report definitions and subscriptions to automate this."

🔶 Technical Highlights
Case Types: Modular design for each process.
Decision Trees: Used for eligibility and approval logic.
Activities & Correspondence Rules: For operator creation and email notifications.
pxSessionTimer: For session management.
Access Control: City-based data restriction.
Escalation Logic: For pending approvals.
🔶 Challenges & Solutions
Challenge	Solution
Session timeout	Used pxSessionTimer in portal header
City-based access	Implemented access roles and filters
Auto approval logic	Used decision trees and premium calculation
Email notifications	Used correspondence rules with dynamic content
Report automation	Used report definitions and subscriptions
🔶 Conclusion
"This project demonstrates how PEGA can be used to automate and streamline insurance workflows. It covers end-to-end functionality from registration to quote approval, with strong focus on user experience, automation, and data security."
