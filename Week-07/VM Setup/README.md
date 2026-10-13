## Here is the Step for the VM Installation

[readme_forVMWorkstation Setup.txt](https://github.com/user-attachments/files/33394610/readme_forVMWorkstation.Setup.txt)
Exact steps — Windows (laptop or pc)

1. Open the official Broadcom Support Portal

Broadcom Support Portal

2. Create an account / Sign in

Click Register if you don't have a Broadcom account.
Complete email verification.
Then sign in.

3. Go to Downloads

After login, look for My Downloads in the portal/dashboard. Broadcom's own instructions specifically say to access VMware Workstation Pro through My Downloads → Free Software Downloads.

4. Find VMware Workstation Pro

Look for:

VMware Workstation Pro

Then select the Windows version, e.g.:

VMware Workstation Pro 17.0 for Windows

Broadcom currently also has newer Workstation releases, so don't worry if the version number you see is newer than 17.x.

5. Select the latest Windows release

Expand the Workstation Pro Windows section and choose the latest available release.

For example, Broadcom's portal has listings such as:

VMware Workstation Pro 25H2 for Windows

The exact version shown to you may differ because Broadcom updates the download portal.

6. Accept the Terms & Conditions

Tick:

I agree to the Terms and Conditions

Then click the download button/arrow.

7. Download the Windows installer

You'll get a Windows installer, typically an .exe file.

Run it → follow the installation wizard → restart Windows if requested.


After Installation:
Open VM-Workstation Pro |-> Open Virtual Machine
                            |-> Tiny Delta
                                |->select .vmx file


                        |-> Edit Virtual Machine setting
                            change memory to 8GB 
                            change  number of processors to 8
s
                        |-> Delta_TinyVM
                            |-> Manage
                                |-> Change Hardware Compatibility
                                     Next-> change version to latest -> next -> select after this virtual machine -> finish


Power on your VM
a dialog box appears, select I moved it. 


Select Delta-> enter password

======================================================
