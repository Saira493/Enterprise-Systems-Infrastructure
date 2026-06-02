# MDT Documentation: Capture and Deploy Windows 11 Image

## Part 1: Prepare MDT Structure
1. **Create Operating System Folder:**
   * Open the **Deployment Workbench**.
   * Navigate to: **Deployment Shares** → **MDT Deployment Share** → **Operating Systems**.
   * Right-click **Operating Systems** → select **New Folder**.
   * Name it: `WINDOWS 11 CAPTURE IMAGE`.
   * Click **Next** → **Next** → **Finish**.
2. **Create Task Sequence Folder:**
   * Navigate to **Task Sequences**.
   * Right-click **Task Sequences** → select **New Folder**.
   * Name it: `WINDOWS CAPTURE IMAGE`.
   * Click **Next** → **Finish**.
3. **Create Subfolder:**
   * Right-click the `WINDOWS CAPTURE IMAGE` folder.
   * Select **New Folder**.
   * Name it: `Windows 11 Capture Image (caedlab1 or IT)`.
   * Click **Next** → **Finish**.

---

## Part 2: Create Capture Task Sequence
4. **Create Sysprep & Capture Task Sequence:**
   * Right-click on your subfolder `Windows 11 Capture Image (caedlab1 or IT)` → select **New Task Sequence**.
   * **Task Sequence ID:** `00008`
   * **Task Sequence Name:** `WINDOWS SYSPREP & CAPTURE`
   * **Template:** Select *Sysprep and Capture* from the dropdown list.
   * **Operating System:** Choose the OS source inside your `WINDOWS 11 CAPTURE IMAGE` folder.
   * **Full Name:** `WINDOWS USER`
   * **Organisation:** `na`
   * Choose to **Skip password** settings.
   * Complete the wizard to **Finish** setup.

---

## Part 3: Modify Task Sequence
5. **Disable Extra Steps:**
   * Right-click on your `WINDOWS SYSPREP & CAPTURE` sequence → select **Properties**.
   * Navigate to the **Task Sequence** tab.
   * Locate and **Disable** the *Execute Sysprep* step under its respective sections to avoid double-processing errors.
   * Click **Apply** and then **OK**.

---

## Part 4: Add Boot Image in WDS
6. **Configure Windows Deployment Services (WDS):**
   * Open **Server Manager** → navigate to **WDS** → right-click and open the main **WDS Management Console**.
   * Expand your server and navigate to the **Boot Images** folder.
   * Right-click **Boot Images** → select **Add Boot Image**.
   * Click **Browse** and point to your deployment share path: `C:\DeploymentShare\Boot`
   * Target and select the Windows PE boot file: `LiteTouchPE_x64.wim`
   * Name it `Windows 11 Capture Image` on both naming tabs.
   * Click through the steps and select **Finish**.

---

## Part 5: Update Deployment Share
7. **Update MDT Engine:**
   * Right-click your root **MDT Deployment Share**.
   * Click **Update Deployment Share**.
   * Select default configuration and complete the generation wizard.

---

## Part 6: Configure Rules
8. **Modify Custom Rules:**
   * Right-click your **Deployment Share** → select **Properties** → navigate to the **Rules** tab.
   * Set or modify the following specific values in the configuration text box:
     ```ini
     OSInstall=NO
     SkipCapture=NO
     ```
   * Click **Apply** and perform another quick deployment share update.

---

## Part 7: Capture Image
9. **Start the Capture Pipeline:**
   * Boot the reference source computer environment over the network via MDT / WDS.
   * When the wizard loads, select the `WINDOWS SYSPREP & CAPTURE` task sequence.
   * Choose the **Capture image** option block.
   * **File name:** `00008 Windows 11 capture image.wim`
   * Begin the automated capture process.
   * **Result:** The deployment engine executes native `Sysprep`, extracts the installation layer, and packages it into a single `.WIM` file.

---

## Part 8: Image Location
10. **Target Destination:**
    * Once the capture process concludes, your newly generated image can be found on your server storage directory at:  
      `C:\DeploymentShare\Captures`

---

## Part 9: Deploy Image
11. **Deployment Architecture Overview:**
    * Import the captured `.WIM` file back into your MDT **Operating Systems** directory tree.
    * Create a brand new **Standard Client Task Sequence** pointing directly to it.
    * Set `OSInstall=YES` inside your Rules properties.
    * Completely update your deployment share and boot target laptops using network PXE.
    * **Key Note:** `OSInstall=NO` is mandatory during a system capture workflow, whereas `OSInstall=YES` is mandatory for deploying images to actual destination hardware client machines.

---

## Part 10: Import Captured Image into MDT
1. **Import Captured File:**
   * In the **Deployment Workbench**, navigate to **Deployment Shares** → **MDT Deployment Share** → **Operating Systems**.
   * Select your dedicated folder: `Windows 11 Capture Image`.
   * Right-click the folder → select **Import Operating System**.
   * Choose the option: **Custom image file**.
   * Click **Next**.
   * **Source File:** Browse to `C:\DeploymentShare\Captures` and select your `00008 Windows 11 capture image.wim` file.
   * Click **Next** → **Next** → **Finish**.
   * **Result:** The custom gold master image layer is successfully available for broad distribution workflows inside MDT.

---

## Part 11: Create Deployment Task Sequence
2. **Create Standard Deployment Engine
