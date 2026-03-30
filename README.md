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

Part 2

Got it — here’s your **step-by-step version with screenshot explanations built into each step**:

---

### **Step-by-Step Lab Actions with Screenshot Explanations**

1. **Viewed user account details**
   Ran `dscl` to display attributes for `testuser02`.
   📸 *Screenshot shows the full directory listing, including the `accountPolicyData` section.*

2. **Checked password status indicators**
   Located `passwordLastSetTime` and `failedLoginCount` in the output.
   📸 *Screenshot highlights `passwordLastSetTime`, which confirms when the password was last changed, and `failedLoginCount: 0`, indicating no failed login attempts.*

3. **Attempted to reset the password**
   Executed `sudo dscl . -passwd /Users/testuser02 NewPassword123!`.
   📸 *Screenshot shows the command being entered in Terminal.*

4. **Encountered authentication requirement**
   The system prompted for the user’s existing password.
   📸 *Screenshot displays the “Permission denied. Please enter user's old password” message, showing the reset was not completed in this attempt.*

5. **Corrected command errors**
   Fixed issues such as a typo in `-passwd` and retried commands.
   📸 *Screenshot shows the incorrect command (`-passwrd`) and resulting usage/help output.*

6. **Confirmed password change indirectly**
   Observed that `passwordLastSetTime` had a recent timestamp.
   📸 *Screenshot again highlights this field, confirming the password had already been successfully changed earlier.*

7. **Verified login capability**
   Tested authentication using `dscl -authonly` or `su`.
   📸 *Screenshot shows either a successful silent return (`dscl`) or successful user switch (`su`), confirming the new password works.*
