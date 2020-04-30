---
description: >-
  A quick description on how you can start the ATM automatically, as soon as the Raspberry Pi has booted.
---

# 🚀 Starting the ATM automatically

If you want that the ATM software starts automatically, every time you boot the Raspberry Pi, you can do this with the systemd file that is part of the software files.

In order to activate the daemon, you first have to copy the file into the right folder on your Rasperry Pi 🍓 and then enable the daemon with these commands:

```text
cd ~/LightningATM
sudo cp LightningATM.service /etc/systemd/system/LightningATM.service
sudo systemctl enable LightningATM.service
```

You can check it the daemon is up and running as well as check the log file with these commands:

```text
# With this command you can check if it is active and running
sudo systemctl status LightningATM.service

# With this command you can check the log/debug file for errors
tail -f ~/.lightningATM/debug.log
```
