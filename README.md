![Release](https://img.shields.io/badge/release-beta-orange.svg)
![Language](https://img.shields.io/badge/made%20with-bash-brightgreen.svg)
![License](https://img.shields.io/badge/license-GPLv3-blue.svg)
![LastUpdate](https://img.shields.io/badge/last%20update-2019%2F09-yellow.svg)

![logo](https://github.com/Leviathan36/SKA/blob/master/IMAGES/logo.png)

## About
SKA is a tool that allows you to implement a very simple and extremely fast karma attack. You can sniff the probe requests to choose the fake AP name or, if you want, you can insert the name of the AP manually (evil twin attack). As soon as the target gets connected to your WLAN you can activate the HTTP redirection and successfully perform a MITM attack.

## Details
The script implements these simple steps:

1. Selection of NICs (Network Interface Cards) for the attack (one for LAN and another for WAN)
2. Capturing the probe-requests to choose the fake AP name (***tcpdump***)
3. Activation of the fake AP (***hostapd*** and ***dnsmasq***)
    
    * the new AP has a DHCP server which provides a valide IP to the target and prevents possible alerts on the victim devices
4. Activation of the HTTP redirection (***iptables***)

    * only HTTP requests are redirect to fake site, while the HTTPS traffic continues to route normally
6. Activation of ***Apache*** server for hosting the phishing site
7. In the end, the script cleans all the changes and restores Apache configuration after the attack.


## Screenshots

<p align="center"><img src="https://github.com/Leviathan36/SKA/blob/master/IMAGES/complete_execution.png" width="65%" height="auto" alt="complete execution"></p>
<br><br>
Press CTRL-C to kill all processes and restore the configuration files.
<br><br>
<p align="center"><img src="https://github.com/Leviathan36/SKA/blob/master/IMAGES/restoring_before_exit.png" width="65%" height="auto" alt="restore configuration files with CTRL-C"></p>


## FAQ
SKA alerts you if you're engaged with some problems with the NetworkManager daemon or Apache configuration file, you could find the answers to your problems in the links given below:

1. [Resolve Network Manager conflict-1](https://rootsh3ll.com/evil-twin-attack/)

    section: "Resolve airmon-ng and Network Manager Conflict"

2. [Resolve Network Manager conflict-2](https://github.com/sensepost/mana/issues/13)

3. [Disable dnsmasq](https://unix.stackexchange.com/questions/257274/how-to-disable-dnsmasq)

#### In summary
1. Disable DNS line in your NetworkManager configuration file (look into /etc/NetworkManager/):

    ```#dns=dnsmasq```

2. Insert the MAC of your wireless adapter between the unmanaged devices to allow ***hostapd*** works properly:

    ```unmanaged-devices=mac:XX:XX:XX:XX:XX:XX```


<br>
<br>

-------------------------------------
## Disclaimer:
Author assume no liability and are not responsible for any misuse or damage caused by this program.

SKA is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details.

## License:
SKA is released under GPLv3 license. See [LICENSE](LICENSE) for more details.
