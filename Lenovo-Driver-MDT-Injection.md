# MDT Documentation: Lenovo Driver Installation and Deployment

## Introduction
This document outlines the process of installing Lenovo storage drivers in Microsoft Deployment Toolkit (MDT) and deploying a Windows image successfully using Windows Deployment Services (WDS).

---

## Part 1: Identify Required Driver
* **Device:** Lenovo V15 G2 ITL (Model 82KB)
* **Required Driver:** Intel Rapid Storage Technology (RST) VMD Driver
* **Important file:** `iaStorVD.inf`

---

## Part 2: Prepare Driver Files
1. Extract the Lenovo driver package.
2. Locate the folder containing the following essential files:
   * `iaStorVD.inf`
   * `iaStorVD.sys`
   * `iaStorVD.cat`
3. Copy these files to a new standalone folder:  
   `C:\Drivers\VMD`

---

## Part 3: Import Driver into MDT
1. Open the **Deployment Workbench**.
2. Navigate to: **Deployment Share** → **Out-of-Box Drivers**.
3. Right-click **Out-of-Box Drivers** → select **New Folder** → Name it: `Lenovo VMD`.
4. Right-click your new `Lenovo VMD` folder → select **Import Drivers**.
5. Browse to the path `C:\Drivers\VMD` and click **Finish**.

---

## Part 4: Create Selection Profile
1. Navigate to **Advanced Configuration** → **Selection Profiles**.
2. Right-click **Selection Profiles** → select **New Selection Profile**.
3. Name the profile: `Lenovo-VMD`.
4. Check the box to select **only** the `Lenovo VMD` folder.
5. Click **Finish**.

---

## Part 5: Configure WinPE Driver Injection
1. Right-click your **Deployment Share** → select **Properties** → navigate to the **Windows PE** tab.
2. Select the **Drivers and Patches** sub-tab.
3. Configure the following settings:
   * **Selection Profile:** `Lenovo-VMD`
   * **Selection Strategy:** Choose *Include all drivers from the selection profile*
4. Click **Apply** → **OK**.

---

## Part 6: Update Deployment Share
1. Right-click your **Deployment Share**.
2. Select **Update Deployment Share**.
3. Choose the option: **Completely regenerate the boot images**.
4. Progress through and **Finish** the update process.

---

## Part 7: Update Boot Image in WDS
1. Open the **WDS Console** (Windows Deployment Services).
2. Navigate to the **Boot Images** folder.
3. Right-click and **Delete** the old, outdated `LiteTouch` boot image.
4. Right-click the **Boot Images** folder → select **Add Boot Image**.
5. Browse to your updated WIM file location:  
   `C:\DeploymentShare\Boot\LiteTouchPE_x64.wim`
6. Complete the wizard to load the new image.

---

## Part 8: Deploy Image to Laptop
1. Boot the Lenovo laptop over the network using **PXE Boot** (Press **F12** at startup).
2. Select the newly updated **LiteTouchPE_x64** boot image.
3. Once the MDT wizard launches, select the target task sequence:  
   `Windows 11 image caedlab1`
4. Continue and complete the deployment wizard.

---

## Result
* **WinPE Alignment:** WinPE successfully loads the integrated Lenovo VMD storage driver.
* **Disk Visibility:** The internal storage disk becomes fully visible to the installer.
* **Completion:** The deployment engine successfully formats the drive and installs the operating system.

## Conclusion
Proper integration of Lenovo storage drivers into the MDT boot image ensures a repeatable, successful deployment and cleanly resolves initial disk detection issues. **Always completely rebuild and refresh your boot images in WDS after making storage driver changes.**
