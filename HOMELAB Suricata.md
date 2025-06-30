**Suricata Setup and Testing Instructions** (Home LAB)

This guide explains how to set up Suricata on a Linux machine and test its detection capabilities using ping and nmap from another device on the same network. 

**1\. Install Suricata** 

**For Ubuntu/Debian:** 

sudo apt update   
sudo apt install suricata \-y 

**2\. Configure Suricata** 

The main configuration file is located at /etc/suricata/suricata.yaml. 

You can run Suricata on a specific network interface (e.g., eth0) with: 

sudo suricata \-c /etc/suricata/suricata.yaml \-i eth0 

*Note: Replace eth0 with the correct network interface name for your system (e.g., ens33, enp0s3). To list available interfaces, use ip addr or ifconfig.* 

 **3\. Start Suricata** 

Enable and start the Suricata service: 

sudo systemctl enable suricata   
sudo systemctl start suricata   
Or, run it directly for testing: 

sudo suricata \-c /etc/suricata/suricata.yaml \-i eth0 


 **4\. Verify Suricata is Running** 

Check the service status: 

sudo systemctl status suricata ( It should say “active(running)” )

Monitor the Suricata log for activity: 

tail \-f /var/log/suricata/fast.log 

**5\. Test Detection with Ping and Nmap** 

From a different machine on the same network: 

* **Ping the Suricata machine:** 

ping \<SURICATA\_IP\> 


* **Scan the Suricata machine with Nmap:** 

nmap \-A \<SURICATA\_IP\>   
or, for a more aggressive scan:   
sudo nmap \-sS \-sV \-O \<SURICATA\_IP\> 


**6\. Review Suricata Alerts** 

After running the ping and nmap tests, check the Suricata log: 

sudo tail \-f /var/log/suricata/fast.log 


You should see alerts or log entries indicating detection of the network activity. 

Notes 

1. SURICATA\_IP is the IP where SURICATA is running (Linux VM in this instance)   
2. I had some trouble running nmap scans from my Mac to my VM machines because of firewall restrictions, but I’m still able to ping them.  
3. I had to adjust the network interface name because my system used a different one than `eth0`. For example, it might be `ens33` or `enp0s3` instead. You can find out what network interfaces your system has by running `ip addr` or `ifconfig`.  
4. [https://suricata.io/docs/](https://suricata.io/docs/) for more documentation\!\! HAVE FUN\!\!

