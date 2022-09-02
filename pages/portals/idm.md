# Identity Management Portal  

The [Identity Management Portal (IDM)](https://idm.ccr.buffalo.edu) provides users with an easy to use interface for the following account management tasks:  


1. [Create a new CCR account](create-a-ccr-system-account)  
2. [Change your password](#when-you-know-your-password)
3. [Reset your password if it was forgotten](#when-you-forgot-your-password)  
4. [See when your password expires](#password-expiration) and other account information  
5. [Upload your public SSH keys](#ssh-keys) to allow for password-less logins to CCR machines  
6. [Manage two-factor authentication](#managing-two-factor-authentication)  


!!! Warning  
    You must be on the UB campus or connected to the [UB VPN](https://buffalo.edu/ubit) from off campus in order to access CCR's portals  

## Create a CCR system account  

UB faculty, staff, students, and those with a UB volunteer appointment are able to create their own CCR account by first authenticating to their UB account.  

!!! Note  
    We can only accept sign-ups from users affiliated with the University at Buffalo.  Do NOT attempt to use the Google or ORCiD iD options as we require authentication against UB systems for verification of your status.  All other users must be either an industry cluster client or collaborating with a UB faculty member and those should be requested through CCR Help.

To create a CCR system account, navigate to the [Identity Management Portal (IDM)](https://idm.ccr.buffalo.edu) and follow these steps:  

1. Click on the `Create Account` link  
2. Click on the `Sign Up` button  
3. After redirecting to the Globus authentication page, select `The State University of New York at Buffalo` from the drop down menu.  (see note above regarding other authentication options)  Then click the `Continue` button  
4. Globus will redirect you to login to UB's authentication system.  Enter your UB username and password (if not already logged in to another UB service)  
5. Through the next several steps, Globus will ask you to link your UB account with an existing Globus account or create a new Globus account and accept their terms of service  
6. You'll then be presented with a request to allow CCR account access to your Globus account info (username, email address, and linked identities).  **Click the `Allow` button**  
7. Once verified, you'll be redirected to the CCR account form which will show your UBIT username and fields to enter your first & last name, email address, and select a password for your CCR account ([See also: Password Requirements](#password-requirements)).  Finally, enter the numbers presented in the Captcha box, and click the `Sign Up` button.  
8. You should see a banner message indicating your account has been created and receive an email with a link to click on.  If you do not receive this email (check your junk/spam folder!), contact CCR Help for assistance.  
9.  Click on the link in the email which redirects you back to the IDM portal.  Click on the `Verify` button.  This completes the verification process and activates your account.  You should see a message indicating the account has been activated AND instructions for [enabling two factor authentication](#enabling-two-factor-authentication).  

!!! Danger  
     Your new CCR account doesn't have access to any CCR resources yet.  After enabling 2FA, use **[Coldfront](coldfront.md) - the CCR resource & allocation management portal** - to manage access to CCR's services.  


## Change your CCR password  

### When you know your password  
To change your existing CCR password, login to the [identity management portal](https://idm.ccr.buffalo.edu) and click on the ``Change Password`` option on the menu.  

### When you forgot your password  

If you forgot your password or can not login using the password you think you set, you can click the `Forgot your password?` link on the [identity management portal](https://idm.ccr.buffalo.edu) home page.  Enter your username and the numbers you see in the Captcha box and press the ``Reset`` button.  You will see a confirmation message in the IDM portal window and an email will be sent to the email address you have set on your CCR account.  Things to keep in mind:  

- You can only change your password once per hour.  If you attempt to change it more that, you will get an error and will need to wait for the hour to pass before attempting to change it again.
- The link contained in the password reset email is valid for 24 hours.  
- If you don't receive an email within an hour, please check your spam or junk folder.  
- When you click on the link contained in the email you'll be redirected to the IDM portal website to select a new password.  If you click on this link and it doesn't work, try to copy the full URL from the email and paste it in your browser.  
- Once you've entered a new password, you should see a confirmation message and will be able to login with the new password.  
- [See also: Password Requirements](#password-requirements)   

!!! Note  
    If you have two factor authentication enabled, you will be required to enter the OTP code from the authentication app you've associated with your CCR account.  This is a 6 digit code that changes every 30 seconds.  

### Password expiration  

CCR passwords expire annually.  You can check when your password expires by logging into the [identity management portal](https://idm.ccr.buffalo.edu) and clicking on the ``Account Information`` option on the menu.  This page also gives you information on what UNIX group your account is a member of and what email address is associated with your CCR account.

If your password is about to expire, set a new one so you don't get locked out.  This can be [done in the IDM portal](#when-you-know-your-password) or you may change your password in the terminal, when logged into one of the cluster login servers.  Use the following commands to get a kerberos ticket and then change your password.   
```  
ccrkinit
Enter OTP Token Value:   
kpasswd  
Enter OTP Token Value:  
Enter new password:  
Enter it again:  
```  

!!! Tip    
    When prompted for ``OTP Token Value`` you'll need to enter your CCR password plus the 6 digit one-time token from the authentication app linked to your CCR account.  There should be no spaces or extra characters between the password and OTP token.   

### Password Requirements  

You will need to select a strong password (or passphrase) that is at least 8 characters and includes a combination of letters and numbers. For information on selecting a strong password, please visit [UBIT's password website](http://www.buffalo.edu/ubit/service-guides/accounts/your-ubitname-account/managing-your-ubitname-and-password/strong-password.html).  


## SSH Keys  

The IDM portal allows users to manage the SSH public keys associated with their CCR account.  SSH key pairs allow us to login without a password using SSH to CCR's login nodes.  We keep our private key on our local machine and upload the matching public key to our CCR account.  Once uploaded, we can login to any CCR server that supports SSH logins.  If your key pair is ever compromised or lost, you can login to the IDM portal and delete it which will immediately revoke it on all CCR's servers.  

!!! Warning    
    You will not be able to upload SSH keys to the IDM portal unless you have two factor authentication enabled.  The `SSH Keys` menu option will not be visible in IDM portal without 2FA enabled    

### Upload SSH Public Key  

To upload your SSH public key, login to the [identity management portal](https://idm.ccr.buffalo.edu) and click on the `SSH Keys` option on the menu.  Click on the `New Key` button and either upload your PUBLIC SSH key or copy the contents of the public key file and paste it into the box.  Then click the `Add` button.  

!!! Note
    It can take up to 15 minutes after uploading your public key to the IDM portal to propagate to all CCR servers before you'll be able to login using your private key  

### Permanently remove SSH keys  

If your key pair is ever compromised or you lose access to it, login to the [identity management portal](https://idm.ccr.buffalo.edu) and delete it, **which will immediately revoke it on all CCR's servers**.  To delete your SSH key from your CCR account, click on the`SSH Keys` option on the menu and click the `Delete` button under the key you want to remove.  You'll be prompted to confirm the deletion request.  

### Creating and using SSH keys  

The creation of a SSH key pair and the method for using it for logins to a linux server are operating system dependent.  We recommend you use your preferred search engine to find one of the many tutorials online for generating and using SSH keys specific to the operating system you're running.  [This site provides everything you could want to know about SSH](https://www.ssh.com/academy).  The CCR cluster login address is `vortex.ccr.buffalo.edu` which is a pool of login servers granting access to our clusters.  

!!! Warning    
    Windows users will need to to convert the SSH key pair generated into an acceptable OpenSSH format in order to use on CCR's systems.  We recommend using [MobaXterm on Windows](https://mobaxterm.mobatek.net/) for creating, converting, & using SSH keys with your CCR account.  


## Managing Two Factor Authentication  

We require users to have two factor authentication (2FA) enabled on their CCR account.  The only service you'll be able to login without 2FA enabled is the IDM portal so that you're able to link an authentication app to your CCR account.  Once 2FA is enabled, you'll use the IDM portal for managing your 2FA settings and devices.  

!!! Danger  
    The UBIT hardware token will NOT work with your CCR account  

### Authentication applications supported for 2FA

Authentication apps that support time-based tokens (TOTP & HOTP) work with CCR accounts.  Options include:  

- **Duo Mobile (for iOS and Android)** - recommended smartphone app as it is currently in use by UBIT for all faculty/staff/student accounts  
- Google Authenticator (for iOS and Android)  
- Authy (for iOS, Android, MacOS, Windows, Linux) - recommended non-smartphone option  
- FreeOTP (for iOS and Android)  
- Microsoft Authenticator (for Windows phones)  
- Sailfish (SailOTP)  

!!! Note  
    Install an authentication app FIRST and have it open on your phone or device prior to enabling 2FA on your CCR account  

### Enabling two factor authentication

==**Save time and problems!  Watch this short demo on how to enable 2FA on your CCR account:**==  

![type:video](https://youtube.com/embed/BDd-J1DAwsw)

!!! Tip  
    For a more detailed, step-by-step tutorial on enabling and using 2FA on your CCR account, we [highly recommend this 8 minute video](https://ub.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=5d2607c9-29bb-45b8-837e-ae32013f375d)  

1.  Login to the [identity management portal](https://idm.ccr.buffalo.edu) and click on the `Two-Factor Auth` menu option  
2.  Click on the `Enable Two-Factor TOTP` button and then click on the `Enable` button when prompted to confirm  
3.  In the authentication app on your smartphone or tablet, click or touch to add a new account. Then scan the QR code shown in the CCR IDM portal.  
**_NOTE_**:  If the device you're using doesn't have a camera, click on the `Show URI` link under the QR code displayed in the IDM portal.  This will display a long code.  Copy this code and paste it into your authentication app.  

==What do I do if I did not see a QR code?  [View your existing OTP tokens](#managing-tokens-for-devices)==

### Logging in with two factor authentication  

Logins to CCR's portals including OnDemand, ColdFront, Lake Effect cloud, IDM, and WebMO require us to enter our CCR password and one time token from our authentication app **together in the password box**.   You must launch the authentication app on your phone or computer, touch or click on the CCR account, and use the one time token generated to login.  These tokens regenerate every 30 seconds.  There should be no spaces or extra characters between the password and OTP token.

!!! Warning    
    **THERE ARE NO PUSH NOTIFICATIONS sent from authentication apps for your CCR account.**

Watch this 50 second video for a demo!  

![type:video](https://youtube.com/embed/g6hWYooFKWE)

### Managing tokens for devices  

You may view all OTP tokens linked to your CCR account by clicking on the `OTP Tokens` menu option. This is where you can delete tokens you no longer need or link additional devices to your account.  To add a new device, click on the `New Token` button and scan the QR code or use the URI link as [described above](#enabling-two-factor-authentication).   If you enabled 2FA and did not see a QR code, you can come here to add a new token.


### Lost access to authentication app  

If you can't login because you no longer have access to the authentication app linked to your CCR account, or somehow the token no longer works, you must contact CCR help to have this reset.  You will be required to prove your identity to us.  Details will be provided by CCR staff.

### Disable two factor authentication  

To disable 2FA on your CCR account, login to the [identity management portal](https://idm.ccr.buffalo.edu) and click on the `Two-Factor Auth` menu option.  Click on the `Disable Two-Factor TOTP` button and when prompted to confirm, click the `Disable` button.  You should now see that 2FA is turned off for your account.  

**REMEMBER**: You will not be able to login to any CCR portals without 2FA enabled!  

!!! Tip  
    Changing phones?  If you won't have access to both devices, disable 2FA on your CCR account prior to swapping phones.  When you get your new phone follow the instructions to [link a new device](#managing-tokens-for-devices) and then [re-enable 2FA](#enabling-two-factor-authentication)  
