#google-authenticator
Google Authenticator PAM module demonstrating two-factor authentication.

##Usage
* Ubuntu users please run this command before building this program:

	sudo apt-get install libpam0g-dev libqrencode3

* Build and install by running "make install".
* Then add the following line at the end of your PAM configuration file.
  Under Ubuntu, you should add that line to three files:
  1. /etc/pam.d/gdm
  2. /etc/pam.d/gnome-screensaver
  3. /etc/pam.d/sshd
	auth required pam_google_authenticator.so pass_unconfigured
* If you use ecryptfs the PAM config line should look like:
	auth required pam_google_authenticator.so pass_unconfigured suffix=.auth
* If you use ecryptfs run these commands as root, replacing username with your user name:
	mkdir /home/username.auth
	mv /home/username/.google_authenticator /home/username.auth/.google_authenticator
	chmod 0400 /home/username.auth
* Make sure that you have this line in /etc/ssh/sshd_config:
	ChallengeResponseAuthentication yes
* Run the "google-authenticator" binary to create a new secret key in your home
  directory.
* If your system supports the "libqrencode" library, you will be shown a QRCode
  that you can scan using the Android/iPhone "Google Authenticator" application.
* If your system does not have this library, you have to manually enter the
  alphanumeric secret key into the Android/iPhone "Google Authenticator" application.
* In either case, after you have added the key, click-and-hold until the context
  menu shows. Then check that the key's verification value matches.
* Each time you log into your system, you will now be prompted for your
  TOTP code (timebased one-time-password) after having entered your normal user
  id and your normal UNIX account password.