# 🏢 Replacing Your Driver Using Zadig

#### Is your Windows machine not detecting your KeepKey, Trezor, or Ledger?

#### We have found that some machines do not have the appropriate default driver settings to successfully recognize a hardware wallet device on beta.shapeshift.com. Not to worry. We have a solution directly from the Windows to help. The following will explain how to use a USB driver installer called Zadig. Installing Zadig

1\. To start, head over to [Zadig](https://zadig.akeo.ie/) Click "Zadig 2.4" and begin the installation.

![](<../../../../.gitbook/assets/image (126).png>)

2\. Once installed, you should see something like this:

![](<../../../../.gitbook/assets/image (50).png>)

### Replacing Your Driver

3\. Click "Options" and select "List All Devices".

![](<../../../../.gitbook/assets/image (209).png>)

4\. You should now see that devices have been detected. Click the drop down caret and select "KeepKey Interface (Interface 0). **For this process, it is important to note that we are NOT going to select KeepKey U2F Interface (Interface 1).**

![](<../../../../.gitbook/assets/image (192).png>)

**5.** To the right of the green arrow use the up or down arrow(s) to navigate to libusbK (v3.0.7.0).

![](<../../../../.gitbook/assets/image (123).png>)

Note: If your current Driver is already libusbK (v3.0.7.0), use the up or down arrow(s) to select WinUSB (v6.1.7600.16385).

Zadig should now look something like this:

![](<../../../../.gitbook/assets/image (219).png>)

6\. Click "Replace Driver".

7\. The driver will begin to install.

![](<../../../../.gitbook/assets/image (19) (1).png>)

![](<../../../../.gitbook/assets/image (198).png>)

8\. You should now see that your current driver has changed to libusbK (or WinUSB depending on which one you replaced.

![](<../../../../.gitbook/assets/image (229).png>)

If you had beta.shapeshift.com open, go ahead and close that down. Restart whichever you were trying to connect your device to and try to pair the KeepKey. If the driver was indeed the issue causing your device to not be detected, you should now see that you are able to connect your KeepKey.
