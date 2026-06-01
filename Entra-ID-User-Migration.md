Entra + User Data Migration Guide
1. Purpose
This guide explains how to move a user from a local account to an Entra (Intune) account and migrate all user data including files, browser data, and passwords.
2. MXToolbox - Check Domain Email Setup
We check MXToolbox to find out where a company’s email is hosted (Google or Microsoft).
Steps:
1. Go to https://mxtoolbox.com
2. Enter domain name (ak.ngo / alkhair.org)
3. Select MX Lookup
4. Click search

Results:
- ASPMX.L.GOOGLE.COM = Google Workspace
- mail.protection.outlook.com = Microsoft 365
3. Important Accounts
Example accounts:
- Intune Admin: Intune@akf.ngo
- Users: Sara@**.ngo, sara@alkhair**
- Check current login (local or Microsoft account)
- Note existing username
- Take backup if needed
5. Prepare Local Administrator
- Login to the PC
- Identify local account
- Create a new local admin account for setup tasks
6. Join Device to Entra
- Go to Settings > Accounts > Access work or school
- Click Connect
- Login using admin account (Intune@***.ngo)
7. Activate Windows
Settings → Activation → Change Product Key (HPDJN-CKJJQ-QYHY3)
8. Setup Microsoft Edge Profile
- Open Edge
- Sign in with user work account
- Turn sync ON (passwords, bookmarks, history) Settings → Profiles → Sync ON
9. Import Browser Data
- Open Edge settings 
- Go to Profiles > Import browser data
- Select Chrome/Brave/Edge
- Import bookmarks, history, passwords
10. Migrate Passwords
- Export passwords from Chrome as CSV
- Export from Chrome: Settings → Password Manager → Export (CSV)
- Import into Edge: Settings > Passwords > Import
11. Clean Browser Profiles
- Remove unused profiles
- Keep only work profile
12. Copy User Data
- Open File Explorer
- Copy files from Desktop, Documents, Downloads, Pictures
- Paste into new user folders e.g. C:/Users

13. Move Data to OneDrive
- Login to OneDrive
- Upload/move files to Desktop, Documents, etc.
- Allow sync
14. Login with Entra User
- Sign out
- Login using Entra account
- Verify files and browser data
15. Additional Setup
- Activate Windows (if needed)
- Confirm Edge sync is ON
16. Common Issues
- Disk space issues
- Missing passwords
- Multiple profiles
- Wrong account login
17. Final Flow
Local check -> Create admin -> Join Entra -> Setup Edge -> Import data -> Copy files -> Login -> Verify
18. Microsoft Entra (Azure AD)
-This is Microsoft identity system
It is used for:
•	User login (Windows, Office 365)
•	Authentication (email, Teams, OneDrive)
Example:
Sara@**.ngo
👉 When user logs into Windows with work email = Entra

💻 Microsoft Intune
👉 This is device management system
It controls:
•	Laptop settings
•	Security policies
•	Apps installation
•	Device compliance

