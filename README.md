# RaspberryPi-Basic-Steps

## 1.) Setting Up Pi
  - Download latest version of [Raspbian](https://downloads.raspberrypi.org/raspbian_full_latest).
  - Format micro-sd card using [SD Card Formatter](https://www.sdcard.org/downloads/formatter/eula_windows/index.html).
  - Write Raspbian image on memory card using [Win32DiskImager](https://sourceforge.net/projects/win32diskimager/files/latest/download).
  
## 2.) SSH, WiFi And VNC
  - Create a new blank file in the root folder and name it as ***ssh*** without any extension. Save it.
  - Create a new file in the root folder and name it as ***wpa_supplicant.conf***.
  - Type Following in that file:
  ```python
    Country=US # Your 2-digit country code
    ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
    network={
      ssid="YOUR_NETWORK_NAME"
      psk="YOUR_PASSWORD"
      key_mgmt=WPA-PSK
    }
  ```
  - Now you can eject the SD card from your computer.
  - Insert your SD card into the Pi.
  - At this point, open PuTTY and try SSHing into the Pi with the address `raspberrypi`
  - Login to pi using login- pi and password- raspberry.
  - At this point, you should run `sudo raspi-config` to expand the file system. 
  - Then select ***7 Advanced options***.
  - Then select ***A1 Expand Filesystem***.
  - When that’s done, select ***Finish*** then ***Yes*** to reboot when prompted.
  - After the reboot, log back in with PuTTY.
  - Enter `sudo raspi-config`.
  - Select ***5 Interfacing options***.
  - Select ***P3 VNC** then ***yes*** then ***OK*** then ***Finish***.
  - Reboot your Pi using ***sudo reboot***.
  - On your PC Open [VNC Viewer](https://www.realvnc.com/download/file/viewer.files/VNC-Viewer-6.19.715-Windows.exe).
  - Enter hostname as ***raspberrypi***, then login.  You will be able to have desktop version of you over VNC
  - Close the ***Welcome to raspberry pi*** screen.
  
## 3.)Starting the server automatically as the pi is plugged in, No need for VNC/PUTTY
  - On the terminal `sudo nano /etc/rc.local`
  - Just before the exit 0, add the following
    ```
    sudo python /home/pi/sensortest.py
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
