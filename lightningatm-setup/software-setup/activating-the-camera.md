# Activating the camera

We will now enable the camera 📸 on the ATM since it is set to `disabled` by default. Whenever you encounter an error in the log file, that is related to the camera, make sure this is setup correctly.

Go into the config menu of the Raspberry Pi with:

```text
sudo raspi-config
```

1. Choose `5 Interfacing Options`
2. Then `P1 Camera`

   It will ask you `Would you like the camera interface to be enabled?`

3. Confirm `<Yes>`
4. Confirm `<Finish>`

   Then you'll be asked `Would you like to reboot now?`

5. Confirm `<Yes>`

As your ATM has restarted, it should now have the camera enabled and be ready to take pictures 🖼 and scan QR codes.

{% hint style="info" %}
If your camera doesn't recognize QR codes, make sure the focus of the camera is properly adjusted. You might need to adjust it manually with a pair of pliers. Check this [link for more details.](https://www.jeffgeerling.com/blog/2017/fixing-blurry-focus-on-some-raspberry-pi-camera-v2-models)
{% endhint %}
