# Assembly and Software

{% embed url="https://www.youtube.com/watch?v=A9JKUQvvmYM" caption="" %}

## Setup process as shown in the video

* Download the Raspbian ATM Image \([https://www.dropbox.com/s/kg5swxhdb9h2a4m/2019-04-08-raspbian-stretch-lightningatm.gz\](https://www.dropbox.com/s/kg5swxhdb9h2a4m/2019-04-08-raspbian-stretch-lightningatm.gz\)\)
* Flash the Image to the SD Card with Etcher.
* Add one file to the /boot folder on the SD Card.
  * Create "wpa\_supplicant.conf" file and add the Wifi credentials.

```text
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
        ssid="You_WiFi_SSID"
        psk="You_WiFi_Password"
}
```

* Connect to it via the console with the user "pi"
  * $ ssh pi@192.168.X.XXX
* Confirm to add the ECDSA key fingerprint with "yes"
* Login with the default password "raspberry"
* Change the default password of the user "pi" to your own
  * $ passwd
  * After confirming the current password, type your new password twice.
* Upgrade the RPi Zero to the newest versions of all Software
  * $ sudo apt update && sudo apt upgrade
* Clone the current version of the LightningATM Software
  * $ git clone [https://github.com/21isenough/LightningATM.git](https://github.com/21isenough/LightningATM.git)
  * $ cd LightningATM
  * $ pip3 install -r requirements.txt
* After reboot connect again to the RPi Zero with your new password.
  * $ ssh pi@192.168.X.XXX

