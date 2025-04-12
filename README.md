# Setting up Privoxy on Raspberry Pi

This guide outlines the steps to install and configure Privoxy, a non-caching web proxy, on a Raspberry Pi. This allows other devices on your network to route their web traffic through the Raspberry Pi.

## Prerequisites

* A Raspberry Pi with Raspberry Pi OS installed.
* A stable network connection (Wi-Fi or Ethernet).
* Basic familiarity with the Linux command line.
* `sudo` privileges.

## Installation

Follow these steps to install and configure Privoxy:

1.  **Update Raspberry Pi Packages:**
    
    This step ensures your Raspberry Pi's software is up-to-date.
    
    ```bash
    $ sudo apt update && sudo apt upgrade -y
    ```
    
2.  **Install Privoxy on Raspberry Pi:**
    
    This command installs the Privoxy package from the Raspberry Pi OS repositories.
    
    ```bash
    $ sudo apt install privoxy -y
    ```
    
3.  **Configure Privoxy on Raspberry Pi:**
    
    By default, Privoxy only listens for connections from the local machine.  This step modifies the configuration to allow connections from other devices on your network.
    
    * Open the Privoxy configuration file:
    
        ```bash
        $ sudo nano /etc/privoxy/config
        ```
    * Inside the `config` file, use "CTRL+W" to search for the following lines:
    
        ```
        listen-address  127.0.0.1:8118
        listen-address  [::1]:8118
        ```
    * Replace those lines with the following line:
    
        ```
        listen-address  :8118
        ```
        
        This tells Privoxy to listen on all network interfaces on port 8118.
    * Save the file: Press "CTRL+X", then "Y", and then "Enter".

4.  **Restart Privoxy:**
    
    This command restarts the Privoxy service to apply the configuration changes.
    
    ```bash
    $ sudo systemctl restart privoxy
    ```
    
5.  **Verify Privoxy Status:**
    
    This command checks if the Privoxy service is running correctly.
    
    ```bash
    $ sudo systemctl status privoxy
    ```

## Using the Proxy

After completing these steps, other devices on your network can use the Raspberry Pi as a proxy server.  You'll need to configure the proxy settings on each device (e.g., in your web browser's network settings) to point to the Raspberry Pi's IP address and port 8118.

For example, if your Raspberry Pi's IP address is `192.168.1.100`, you would set the proxy server address to `192.168.1.100` and the port to `8118`.

## Important Notes

* **Security:** By default, Privoxy is an *open proxy*, meaning any device that can reach your Raspberry Pi can use it.  This can be a security risk if your Raspberry Pi is accessible from the public internet.  Consider setting up firewall rules or authentication if you need to expose your proxy to a wider network.
* **Static IP:** It's recommended to assign a static IP address to your Raspberry Pi on your local network.  This will prevent its IP address from changing, which would require you to reconfigure the proxy settings on your other devices.
* **Configuration:** Privoxy has many advanced configuration options.  See the official Privoxy documentation for details: [https://www.privoxy.org/](https://www.privoxy.org/)
