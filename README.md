# RaspberryPi-Basic-Steps

## 1.) Setting Up Pi Zero
  - Download latest version of [Raspbian](https://downloads.raspberrypi.org/raspbian_full_latest).
  - Format micro-sd card using [SD Card Formatter](https://www.sdcard.org/downloads/formatter/eula_windows/index.html).
  - Write Raspbian image on memory card using [Win32DiskImager](https://sourceforge.net/projects/win32diskimager/files/latest/download).
  
## 2.) Sharing ethernet connection over USB
  - Navigate to the root directory of the micro SD card and open the file ***config.txt*** with Wordpad.
  - Scroll down to the bottom of the file and add `dtoverlay=dwc2` to a new line
  - Save and exit the ***config.txt*** file.
  - Now open the ***cmdline.txt*** file with Notepad. Make sure “Word Wrap” is off to view the file as a single line. You don’t want to add any line breaks to this file. All of the commands need to be in a single line. If you use Wordpad to edit this file, you may create unintentional line breaks, so using Notepad is best. Scroll across the line and find the command `rootwait`.  After the `rootwait` command, type `modules-load=dwc2,g_ether`
  - Save and exit the ***cmdline.txt*** file.
  - Create a new blank file in the root folder and name it as ***ssh*** without any extension. Save it.
  - Now you can eject the SD card from your computer.
  - Insert your SD card into the Pi Zero, and plug your micro USB to USB adapter (or cable) into the Pi’s micro USB port (not the power connection), and the other end into your computer.
  - You’ll see that Windows recognizes the Pi, and will attempt to setup the device.
  - At this point, open PuTTY and try SSHing into the Pi with the address `raspberrypi`
  - Raspberry pi Device should be recognized as RNDIS/ethernet gadget on windows device manager.
  - Login to pi using login- pi and password- raspberry.
  - At this point, you should run `sudo raspi-config` to expand the file system. 
  - Then select ***7 Advanced options***.
  - Then select ***A1 Expand Filesystem***.
  - When that’s done, select ***Finish*** then ***Yes*** to reboot when prompted.
  - After the reboot, log back in with PuTTY.
  - On your PC navigate to the ***Network Connections*** window.
  - Your Pi will show up as a separate network connection. It will say ***USB Ethernet/RNDIS gadget*** under the connection name.
  - Now you should decide which connection you want your Pi to access the Internet over (i.e. WiFi or Ethernet). I want my Pi to access the internet over my computer’s WiFi connection, so I’ll need to enable my WiFi connection to allow sharing. Right click on the connection you want to use, then select ***Properties***.
  - In the WiFi Properties window, click on the ***Sharing*** tab.
  - Click the box that says ***Allow other network users to connect through this computer’s Internet connection***, then click the drop down menu below that. Find the network connection given to your Pi, select it, then click OK.
  - Now reboot your Pi and log back into it with PuTTY.
  - Enter `sudo ping www.google.com` to test the connection further, and you should see that your Pi has internet access!
  - Enter `sudo raspi-config`.
  - Select ***5 Interfacing options***.
  - Select ***P3 VNC** then ***yes*** then ***OK*** then ***Finish***.
  - Reboot your Pi using ***sudo reboot***.
  - On your PC Open [VNC Viewer](https://www.realvnc.com/download/file/viewer.files/VNC-Viewer-6.19.715-Windows.exe).
  - Enter hostname as ***raspberrypi***, then login.  You will be able to have desktop version of you over VNC
  - Close the ***Welcome to raspberry pi*** screen.
  
## 3.)Starting the server automatically as the piZero is plugged in, No need for VNC/PUTTY
  - On the terminal `sudo nano /etc/rc.local`
  - Just before the exit 0, add the following
    ```
    sudo node /home/pi/nfc-chat/backend/Server.js &
    sudo npm start --prefix /home/pi/nfc-chat/frontend &
    ```
  - Now on the next reboot, Server and App will start on its own.
  
## 4.) Creating  PI image that can be copied to other SD cards and used.
  - When your Pi is set up exactly as you want, shut it down and remove its SD card.
  - Plug the SD card into your computer, download [Win32DiskImager](https://sourceforge.net/projects/win32diskimager/files/latest/download) (if you haven’t already).
  - In Win32 Disk Imager, click the blue folder button to select the location for the image you’re going to create and give your image a name.
  - Next, choose your Pi from the “Device” dropdown. If your Pi has multiple partitions, choose the first one—but don’t worry, this process will clone the entire card, not just the individual partition.
  - When you’re done, click the “Read” button. This reads the SD card’s data, turns it into an image, and saves that image at the specified location. Note that this process can take a while. As in, up to an hour or more depending on the size of your SD card.
  - When that’s finished, pop the card back into your Pi and continue as normal! That project is now backed up to your PC.
  - To restore the card, first format the sd card, using sd card formatter.
  - With your erased card still inserted into your PC, open Win32 Disk Imager again. This time, click the blue folder and navigate to your saved image. Choose your SD card from the dropdown the same way you did before.
  - When you’ve got it set up, click the “Write” button. This overwrites the SD card’s data with data from the cloned image.
  - ***Note*** that you’ll probably need to use the same SD card—or at least the same model of SD card—for best results.
