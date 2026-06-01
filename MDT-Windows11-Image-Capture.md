MDT Documentation: Capture and 
Deploy Windows 11 Image 
Part 1: Prepare MDT Structure 
1. Create Operating System Folder - Open Deployment Workbench - Go to Deployment Shares → MDT Deployment Share → Operating Systems - Right-click → New Folder - Name: WINDOWS 11 CAPTURE IMAGE - Click Next → Next → Finish 
2. Create Task Sequence Folder - Go to Task Sequences - Right-click → New Folder - Name: WINDOWS CAPTURE IMAGE - Click Next → Finish 
3. Create Subfolder - Right-click WINDOWS CAPTURE IMAGE - Select New Folder - Name: Windows 11 Capture Image (caedlab1 or IT) - Click Next → Finish 
Part 2: Create Capture Task Sequence 
4. Create Sysprep & Capture Task Sequence - Right-click on WINDOWS 11 CAPTURE IMAGE (CAEDLAB1)  → New Task Sequence - ID: 00008 - Name: WINDOWS SYSPREP & CAPTURE - Select Sysprep and Capture - Choose OS from WINDOWS 11 CAPTURE IMAGE - Enter Name: WINDOWS USER,  - Organisation: na - Skip password - Finish setup 
Part 3: Modify Task Sequence 
5. Disable Extra Steps - Right-click on WINDOWS SYSPREP & CAPTURE  → Properties - Task Sequence tab - Disable Execute Sysprep step under sections 
- Apply and OK 
Part 4: Add Boot Image in WDS 
6. Configure WDS - Open Server Manager → WDS → right-click and search for WDS MD server console - Open WDS Console - Go to Boot Images -> right -click on Add Boot Image - Add Boot Image - Browse to C:\DeploymentShare\Boot - Select LiteTouchPE_x64.wim - Name it Windows 11 Capture Image same name on both tabs - Finish 
Part 5: Update Deployment Share 
7. Update MDT - Right-click Deployment Share - Click Update Deployment Share - Complete wizard 
Part 6: Configure Rules 
8. Modify Rules - Go to Properties → Rules - Set: 
OSInstall=NO 
SkipCapture=NO - Apply and update share 
Part 7: Capture Image 
9. Start Capture - Boot machine via MDT - Select WINDOWS SYSPREP & CAPTURE - Choose Capture image option - File name: 00008 Windows 11 capture image.wim - Begin process 
Result: - System runs Sysprep - Captures image - Saves .WIM file 
Part 8: Image Location 
10. Location - C:\DeploymentShare\Captures 
Part 9: Deploy Image 
11. Deployment - Import .WIM into Operating Systems - Create Standard Client Task Sequence - Select the captured image - Update deployment share - Deploy to laptop 
Notes: - OSInstall=NO used for capture - OSInstall=YES used for deployment - Captured image includes installed apps and settings 
Part 10: Import Captured Image into MDT 
1. Import Captured Image - Open Deployment Workbench - Navigate to Deployment Shares → MDT Deployment Share → Operating Systems - Select the folder: Windows 11 Capture Image - Right-click → Import Operating System - Choose: Custom image file - Click Next - Browse to the location: 
C:\DeploymentShare\Captures - Select the captured .WIM file - Click Next → Next → Finish 
Result: 
The captured image is now available in MDT under Operating Systems. 
Part 11: Create Deployment Task Sequence 
2. Create Standard Deployment Task Sequence 
- Go to Task Sequences - Select your deployment folder - Right-click → New Task Sequence 
Enter the following details: - Task Sequence ID: 00009 - Task Sequence Name: Windows 11 Capture Image (caedlab1) 
Click Next - Select: Standard Client Task Sequence - Click Next - Choose the imported captured image (.WIM file) - Click Next → Next 
Enter user details: - Full Name: WINDOWS USER - Organisation: na 
Click Next → Finish 
3. Verify Task Sequence - Right-click the created Task Sequence - Select Properties - Go to Task Sequence tab - Ensure all steps are correctly configured - Click Apply → OK 
Part 12: Configure Rules for Deployment 
4. Modify MDT Rules - Go to Deployment Share → Properties → Rules tab 
Set the following values: 
OSInstall=YES 
SkipLocaleSelection=YES - Click Apply → OK 
5. Update Deployment Share - Right-click Deployment Share - Select Update Deployment Share - Complete the wizard 
Final Result: - Captured image is imported into MDT - Deployment Task Sequence is created - MDT is configured for OS installation - System is ready for deployment to new devices 
Summary: - Import captured .WIM file 
- Create Standard Client Task Sequence - Configure rules for deployment (OSInstall=YES) - Update MDT - Deploy image to target machine 
IMPORTANT NOTE:  
Choose DO NOT CAPTURE -> Next -> Don't select any app because those apps are already 
capture in an image.  
