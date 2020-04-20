# Activating the camera

We will now enable the camera on the ATM since it is set to `disabled` by default. Whenever you encounter an error in the log file, that is related to the camera, make sure this is setup correctly. 

Go into the config menu of the Raspberry Pi with:

```
sudo raspi-config
```

1. Choose `5 Interfacing Options`
2. Then `P1 Camera`
It will ask you `Would you like the camera interface to be enabled?`
3. Confirm `<Yes>`
4. Confirm `<Finish>`
Then you'll be asked `Would you like to reboot now?`
5. Confirm `<Yes>`

As your ATM has restarted, it shoudl now have the camera enabled and be ready to take pictures and scan QR codes. 

