MDT Documentation: Lenovo Driver Installation and Deployment

Introduction
This document outlines the process of installing Lenovo storage drivers in Microsoft Deployment Toolkit (MDT) and deploying a Windows image successfully using Windows Deployment Services (WDS).

Part 1: Identify Required Driver
- Device: Lenovo V15 G2 ITL (Model 82KB)
- Required Driver: Intel Rapid Storage Technology (RST) VMD Driver
- Important file: iaStorVD.inf

Part 2: Prepare Driver Files
1. Extract Lenovo driver package.
2. Locate folder containing:
   - iaStorVD.inf
   - iaStorVD.sys
   - iaStorVD.cat
3. Copy these files to a new folder:
   C:\Drivers\VMD

Part 3: Import Driver into MDT
1. Open Deployment Workbench.
2. Navigate to: Deployment Share → Out-of-Box Drivers.
3. Right-click → New Folder → Name: Lenovo VMD.
4. Right-click folder → Import Drivers.
5. Browse to: C:\Drivers\VMD → Finish.

Part 4: Create Selection Profile
1. Go to Advanced Configuration → Selection Profiles.
2. Right-click → New Selection Profile.
3. Name: Lenovo-VMD.
4. Select only the Lenovo VMD folder.
5. Finish.

Part 5: Configure WinPE Driver Injection
1. Go to Deployment Share → Properties → Windows PE tab.
2. Select Drivers tab.
3. Set:
   - Selection Profile: Lenovo-VMD
   - Enable: Include all drivers from selection profile
4. Click Apply → OK.

Part 6: Update Deployment Share
1. Right-click Deployment Share.
2. Select Update Deployment Share.
3. Choose: Completely regenerate boot images.
4. Finish update process.

Part 7: Update Boot Image in WDS
1. Open WDS Console.
2. Navigate to Boot Images.
3. Delete old LiteTouch boot image.
4. Right-click → Add Boot Image.
5. Browse to: C:\DeploymentShare\Boot\LiteTouchPE_x64.wim
6. Complete wizard.

Part 8: Deploy Image to Laptop
1. Boot Lenovo laptop using PXE (F12).
2. Select new LiteTouchPE_x64 boot image.
3. MDT wizard launches.
4. Select task sequence:
   Windows 11 image caedlab1
5. Continue deployment.

Result
- WinPE loads Lenovo VMD storage driver.
- Disk becomes visible.
- System successfully formats and installs Windows.

Conclusion
Proper integration of Lenovo storage drivers into MDT boot image ensures successful deployment and resolves disk detection issues. Always rebuild boot images after driver changes.

