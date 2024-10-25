# Identity Management Portal  

CCR's Identity Management Portal (IDM) provides users with an easy to use
interface for managing their CCR user accounts. Existing users can access the
IDM portal [here](https://idm.ccr.buffalo.edu). Don't have a CCR user account
yet? [see here](../getting-access.md) for more info on creating an account.
Common account management tasks include:  

- [Changing your password](#change-your-ccr-password)
- [Reset your password if it was forgotten](#change-your-ccr-password)  
- [Manage two factor authentication](#manage-two-factor-authentication)  
- [Manage SSH keys](#manage-ssh-keys)


!!! Warning "VPN Required" 
    Access to the IDM portal is restricted to UB and Roswell Park networks
    (either on campus or connected to their VPN services). [See here](../getting-access.md#vpn-access)

## Change your CCR password  

To change your existing CCR password, login to the [identity management
portal](https://idm.ccr.buffalo.edu) and click on the `Password` option on the
menu.  Enter your current password, then enter your new password and confirm it
before clicking the `Update` button.  

If you forgot your password or can not login using the password you think you
set, navigate to the [identity management portal](https://idm.ccr.buffalo.edu),
enter your username and click the `Next` button.  Click the `Forgot password?`
link.  You'll be asked for your username and to enter the numbers seen in the
captcha picture.  Then click the `Submit` button.  You will receive an email
with further instructions.

!!! Warning "Getting an error?"  
    Occassionally during a password change you might see an error like `something bad happened` with instructions to contact an administrator.  We apologize for this inconvenience!  The fact is that the password reset process completed successfully and you can go forward with using the new password.  If you see any errors after this point, please clear your browser cache and restart your browser.  

Things to keep in mind:  

- You can only change your password once per hour.  If you attempt to change it
  more that, you will get an error and will need to wait for the hour to pass
  before attempting to change it again.
- The link contained in the password reset email is valid for 15 minutes.  
- If you don't receive an email promptly, please check your spam or junk folder.  
- If you click on this link and it doesn't work, try to copy the full URL from the end of the email and paste it in your browser.  
- You will need to select a strong password (or passphrase) that is at least 8 characters and includes a combination of letters and numbers. For information on selecting a strong password, please visit [UBIT's password website](http://www.buffalo.edu/ubit/service-guides/accounts/your-ubitname-account/managing-your-ubitname-and-password/strong-password.html).  

!!! Note  
    If you have two factor authentication enabled, you will be required to
    enter the OTP code from the authentication app you've associated with your
    CCR account. This is a 6 digit code that changes every 30 seconds.  

## Manage Two Factor Authentication  

We require users to have two factor authentication (2FA) enabled on their CCR
account.  The only service you'll be able to login without 2FA enabled is the
IDM portal so that you're able to link an authenticator app to your account.
Once 2FA is enabled, you can use the IDM portal for managing your 2FA settings
and devices. For more detailed information on 2FA [please see here](../2fa.md)

## Manage SSH Keys  

The IDM portal allows users to manage the SSH public keys associated with their
CCR account. SSH key pairs allow you to login using SSH to CCR's login nodes.
The private ssh key stays on our local machine and the matching public key is
uploaded to your CCR account.

You can add new ssh keys by [logging into the IDM
portal](https://idm.ccr.buffalo.edu) and clicking on the `SSH Keys` menu
option. If your ssh key pair is ever compromised or lost, you can login to the
IDM portal and delete it which will immediately revoke it on all CCR's servers.

!!! Warning "Two factor auth required"
    You will not be able to upload SSH keys to the IDM portal unless you have
    two factor authentication enabled.  

For more information on creating ssh keys and logging in to the login nodes, [see here](../hpc/login.md#connecting-with-ssh)
