# CVE-2019-11539

### Original Discovery: [Orange Tsai](https://twitter.com/orange_8361), [Meh Chang](https://twitter.com/mehqq_)

### Authors: [Justin Wagner](https://twitter.com/0xDezzy), [Alyssa Herrera](https://twitter.com/Alyssa_Herrera_)

### Thanks to: [Orange](https://twitter.com/orange_8361), [Meh Chang](https://twitter.com/mehqq_), [Rich Warren](https://twitter.com/buffaloverflow), [Alyssa](https://twitter.com/Alyssa_Herrera_), [Mimir](https://twitter.com/XMPPWocky)
## Vulnerability Description
In Pulse Secure Pulse Connect Secure version 9.0RX before 9.0R3.4, 8.3RX before 8.3R7.1, 8.2RX before 8.2R12.1, and 8.1RX before 8.1R15.1 and Pulse Policy Secure version 9.0RX before 9.0R3.2, 5.4RX before 5.4R7.1, 5.3RX before 5.3R12.1, 5.2RX before 5.2R12.1, and 5.1RX before 5.1R15.1, the admin web interface allows an authenticated attacker to inject and execute commands.

## Exploit Description
This exploit takes advantage of the [Post-Auth Remote Code Execution Vulnerability](https://nvd.nist.gov/vuln/detail/CVE-2019-11539) and modifies the SSH configuration to allow a user to log in as root on the VPN appliance itself. It will download a new ssh configuration and authorized_keys file, backup the original, then overwrite the old files. Once this is done, it will send a SIGHUP to sshd-ive, restarting the process and loading the new configuration.

## Configuration
To use this exploit, you will need to modify the following:

The Host you are targeting:
```
...
host = 'REPLACE-WITH-IP-OR-FQDN' # Host to exploit
...
```
The admin login credentials for the VPN appliance:
```
# Login Credentials
user = 'admin' # Default Username
password = 'password' # Default Password
```
And the host to download the files from:
```
# Necessary for Curl
downloadHost = '' # IP or FQDN for host running webserver
port = '' # Port where web service is running. Needs to be a string, hence the quotes.
```

Once that is modified, you should be able to run the exploit without any issues. If the system is read only, you will need to modify the code and mount the system as read write. I will not do this for you. You need to have the knowledge of the system you are targeting.

A demo can be seen below:

## Demo
[![Image alt text](http://img.youtube.com/vi/HyWcRrJt1g0/0.jpg)](https://www.youtube.com/watch?v=HyWcRrJt1g0)

## Blog Post By [Alyssa Herrera](https://twitter.com/Alyssa_Herrera_)
You can find the blog post that Alyssa and I worked on [here](https://medium.com/@alyssa.o.herrera/pulse-secure-ssl-vpn-post-auth-rce-to-ssh-shell-2b497d35c35b)
