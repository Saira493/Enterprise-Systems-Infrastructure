 GCPW Setup Documentation (Simple Guide)
1. What is GCPW?
GCPW (Google Credential Provider for Windows) allows users to sign into a Windows computer using their Google Workspace account instead of a local or Microsoft account.
2. Why do we use GCPW?
- Control who can log into company computers
- Use company Google accounts instead of local accounts
- Enable admin control from Google Admin Console
- Block personal Gmail accounts
3. Why do we need a domain?
A domain (e.g. tar.co.uk) represents your organisation. It ensures only company-managed accounts can log in and allows admin control and security policies.
4. How to Set Up Google Workspace
- Go to https://workspace.google.com
- Enter your domain
- Create admin account (e.g. admin@tar.co.uk)
- Verify domain using DNS TXT record
- Add users in admin.google.com
5. How to Install GCPW on Windows 11
- https://admin.google.com
- Login with your admin account admin@tar.co.uk
- Devices → Mobile & endpoints → Settings → Windows
- Google Credential Provider for Windows (GCPW)
-Go to Permitted Domains
-Add your domain
-tar.co.uk
-Go to, Devices → Windows → GCPW Setup-> doenload
-Save

7. Restart the PC to Login, If it says restricted then run the cmd given below. 
8. Configure Allowed Domain
Run the command below to restrict login to your domain: 
First type : regedit 

Then type:
reg add "HKLM\Software\Google\GCPW" /v domains_allowed_to_login /t REG_SZ /d "tar.co.uk" /f


7. What does the command do?
It ensures only users with emails from tarbiyyah.co.uk can log into the device.
8. When to use the command?
- During new device setup
- Before first login
- During company rollout
- When enforcing security restrictions
9. What happens after setup?
Users can log in using their Google Workspace account and personal accounts are blocked.
10. Common Mistakes
- Wrong domain entered
- Domain not verified
- Users not created in Admin Console
- Command not run before login
