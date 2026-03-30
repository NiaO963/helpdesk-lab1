# helpdesk-lab1
In this lab, I will be simulating the process of a real-world Level IT Support help desk environment, specifically involving my ability to receive, triage, troubleshoot and resolve common end-user IT issues. 
TICKET-001 — User Account Creation & Password Reset on Shared Workstation
Ticket Details
TICKET-001 Date Submitted: 2026-03-30 Submitted By Site Supervisor — Shared Workstation Area Priority: Medium Category: User Account Management Status: ✅ Resolved Assigned To: L1 IT Support Technician

📋 Reported Issue

"We have a new staff member starting today on the shared workstation. We also need the previous user's password reset — they've been locked out and can't log in to complete their shift reports."


🔍 Troubleshooting Steps
Step 1 — Navigate to User Management

Opened Apple Menu → System Settings → Users & Groups
Confirmed existing accounts on the machine
Identified that a new Standard user account needed to be created for the incoming staff member

Step 2 — Create New Standard User Account

Clicked "Add Account"
Configured the new account with the following settings:

Account Type: Standard (non-admin, appropriate for shared workstation end users)
Full Name: TestUser02
Account Name: testuser02
Set a secure initial password and confirmed it in the Verify field


Clicked "Create User" to finalize
Confirmed TestUser02 appeared under "Other Users" in the sidebar

📷 Screenshot 1: New account creation form showing Standard account type and user details
📷 Screenshot 2: Users & Groups panel confirming TestUser02 successfully created
Step 3 — Reset Password for Locked Out User

Selected TestUser02 in the Users & Groups panel
Clicked "Reset Password..."
Entered and verified the new password in the dialog box
Noted the macOS keychain warning — advised user that their login keychain password would need to be updated separately via Keychain Access in Utilities if needed
Clicked "Change Password" to apply

📷 Screenshot 3: Password reset dialog showing new password entry and keychain advisory notice
Step 4 — Verify Account via Terminal

Opened Terminal and ran the following command to confirm the account existed at the system level:

bash  dscl . list /Users | grep -v '_'

Output confirmed testuser02 was present alongside other system accounts:

  daemon
  Guest
  livvy
  nobody
  root
  testuser02
📷 Screenshot 4: Terminal output confirming testuser02 exists on the system

🔎 Root Cause
End user was locked out of their local account due to a forgotten password. A new account was also required for an incoming staff member on the shared workstation. Both tasks were handled through macOS Users & Groups with admin privileges.

✅ Resolution
Created new Standard user account TestUser02 → reset password for locked out user → verified account existence via Terminal dscl command → confirmed with supervisor that both users could now log in successfully.

📝 Notes & Follow-Up

Standard account type was used intentionally — end users on shared workstations should not have admin rights per least-privilege best practices
macOS keychain password is separate from login password — if user reports keychain prompts after password reset, direct them to Keychain Access in the Utilities folder
Documented new account name for IT records
Recommended periodic review of shared workstation user accounts to remove stale accounts
