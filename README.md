..
Step 1: Update Raspberry Pi Packages

$ sudo apt update && sudo apt upgrade -y

Step 2: Install Privoxy on Raspberry Pi

$ sudo apt install privoxy -y

Step 3: Configure Privoxy on Raspberry Pi

Once your complete the Privoxy installation on your device, you have to do a change in its configuration file and for that you first need to open the configuration file through following command:

$ sudo nano /etc/privoxy/config

With the file open, you have to find the following lines using “CTRL+W” keys.

listen-address  127.0.0.1:8118
listen-address  [::1]:8118

Replace the above lines with the following line so that it will allow the outside device to access your proxy server.

listen-address :8118

After applying the changes, save the file using the “CTRL+X” key with adding Y afterwards and press enter in the last to go back to the terminal.

$ sudo systemctl restart privoxy

After the restart, ensure that Privoxy server is running on your device using the following command:

$ sudo systemctl status privoxy
