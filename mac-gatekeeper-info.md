# Mac gatekeeper

To disable Mac gatekeeper for a specific app when getting the error
"X cannot be opened because the developer cannot be verified"

    sudo xattr -dr com.apple.quarantine <base path of application>

# Allowing Apps from Anywhere on MacOS Sonoma/Ventura

The xattr command is specific to the application dir it runs on, while the spctl method is global for all applications (thus much higher risk). Do the following at your own risk!

1. Quit out of System Settings if it is currently open
2. Open Terminal and type
   
   ```
   sudo spctl --master-disable
   ```
   
4. You will need to enter the sudo password
5. Open System Settings, go to Privacy & Security, and scroll down to the Security section
6. Under 'Allow apps downloaded from' change to Anywhere

You can keep this enabled, or toggle the other options. The “Anywhere” option for apps will remain enabled and available in System Settings until disabled again via command line.

If you share your Mac with someone else it might be wise to get rid of the Anywhere option. To hide it again, you’ll need to go to Terminal again, and this time type:

```
sudo spctl –master-enable
```
