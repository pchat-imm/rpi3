# RPI3 & RPI4
to use raspberry pi, with monitor, windows, mac, and ubuntu

## Table of contents

1. [installation](#installation) \
2. [(optional) sharing WiFi](#sharingWiFi) \ 
3. [Total Setup to notebook](#SetupNotebook) \
4. [ssh](#ssh) \
5. [RemoteVNC](#RemoteVNC) \
6. [add Wi-Fi for RPI](#RPIWiFIWPA) \
7. [Use case 1: Quectel](#rpi-quectel)

## 1.installation <a name = "installation"></a>
### 1.1. Pi Imager
- Download Raspberry Pi Imager https://www.raspberrypi.com/software/
    - select device as RPI3
### 1.2. RPI3 (Windows OS)
- in case install in Windows: https://medium.com/@chatchamonphoojaroenchanachai/%E0%B8%81%E0%B8%B2%E0%B8%A3%E0%B9%83%E0%B8%8A%E0%B9%89%E0%B8%87%E0%B8%B2%E0%B8%99%E0%B8%9A%E0%B8%AD%E0%B8%A3%E0%B9%8C%E0%B8%94-raspberry-pi-3-model-b-rpi-4ca6a0f5ce01
### 1.3. RPI4
<img src="https://github.com/pchat-imm/rpi3/assets/40858099/0552b5d9-acb5-483f-b4fb-3524ccfc9702" width="50%" height="50%"/> 
Equipment for access the RPI for the first time: 

- RPI4 Power Cord (Type C)
- RPI4 board
- SD card 32 GB
- LAN cable (connect to CPE)
- CPE
- HDMI to Micro USB (connect to monitor)
- Keyboard (connect to RPI board)
- Mouse (connect to RPI board)
- and Monitor (connect between HDMI (monitor) and micro USB (to RPI4))

## (optional) 2. sharing WiFi <a name = "sharingWiFi"></a>
- keep in mind that if the board can connect to WiFi, it will **blink yellow led**
- **In case you do not have CPE**, you need to connect LAN to your computer to share the internet so that we can update the RPI for the first time

### 2.1 Windows
- `control panel -> changing adapter option -> Wi-Fi -> Properties -> Sharing -> allow other networks users to connect through this computer's internet connection`
- `control panel -> changing adapter option -> Wi-Fi -> Properties -> TCP/IPv4 
    -> IP address: 192.168.137.1
    -> Subnet mask: 255.255.255.0`
<img src="https://github.com/pchat-imm/rpi3/assets/40858099/3d8f4c9a-287f-4431-8a7a-48449f931aa8" width="30%" height="30%"/>

### 2.2 MAC OS
- `setting -> WiFi -> TCP/IP: Using DHCP`
and if the connection turns out correct it will show like this
<img src="https://github.com/pchat-imm/rpi3/assets/40858099/cecee855-0056-4700-8d85-b2421ddcdfa0" width="40%" height="40%"/>
<img src="https://github.com/pchat-imm/rpi3/assets/40858099/c02f471f-ba30-4e7e-886e-e369172196ba" width="40%" height="40%"/>
 

## 3. Total Setup to notebook <a name = "SetupNotebook"></a>
input: SD card, LAN to router, power adapter to computer \
<img src="https://github.com/pchat-imm/rpi3/assets/40858099/797e4f5e-98aa-4c91-8722-651dbcf5f473" width="50%" height="50%"/>

- Input: SD card, LAN to router, power adapter to computer
- This is not for first time using the RPI!!! 


## 4. SSH <a name = "ssh"></a>
### 4.0 check IP address (so that can ssh to the RPI board)
- in case your rpi is headless (no monitor), you can connect the rpi to the computer and try to find its ip address. \
```
>> arp -a
? (192.168.1.1) at 14:13:46:ae:3d:38 on en0 ifscope [ethernet]
? (192.168.1.33) at 8:54:bb:e5:18:b9 on en0 ifscope [ethernet]
? (192.168.1.36) at b8:27:eb:2a:da:e9 on en0 ifscope [ethernet]
mdns.mcast.net (224.0.0.251) at 1:0:5e:0:0:fb on en0 ifscope permanent [ethernet]
? (239.255.255.250) at 1:0:5e:7f:ff:fa on en0 ifscope permanent [ethernet]
```
and you may ping every address that is showing \
or tested in ping raspberrypi.local and see the address \
```
>> ping raspberrypi.local
PING raspberrypi.local (192.168.1.36): 56 data bytes
64 bytes from 192.168.1.36: icmp_seq=0 ttl=64 time=131.686 ms
64 bytes from 192.168.1.36: icmp_seq=1 ttl=64 time=10.251 ms
64 bytes from 192.168.1.36: icmp_seq=2 ttl=64 time=10.259 ms
64 bytes from 192.168.1.36: icmp_seq=3 ttl=64 time=10.597 ms
```
therefore, the raspberry pi connect to `192.168.1.36` \
when you have address, you can ssh to the rpi

### 4.1. access SSH through Putty (Windows)
<img src="https://github.com/pchat-imm/rpi3/assets/40858099/3d7644c3-a201-4d07-a4e8-b274008c912f" width="35%" height="35%"/>
- IP address: 192.168.1.36, Port: 22, SSH

### 4.2 access SSH through terminal (MAC OS)
my username is `chatchamon`, and password `12345678`
```
>> ssh chatchamon@192.168.1.36
chatchamon@192.168.1.36's password: 
Linux raspberrypi 6.1.21-v7+ #1642 SMP Mon Apr  3 17:20:52 BST 2023 armv7l

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Thu Apr  4 08:01:31 2024
chatchamon@raspberrypi:~ $
```

## 5. RemoteVNC <a name = "RemoteVNC"></a>
### 5.0 install VNC server on RPI
```
>> Sudo apt update
>> Sudo apt install realvnc-vnc-server
```
### 5.1 Setup VNC on RPI
in ssh (putty - Windows OS, terminal - MAC OS)
```
>> sudo raspi-config
```
<img src="https://github.com/pchat-imm/rpi3/assets/40858099/169b56dc-170d-4b66-b380-b6bc7574129c" width="40%" height="40%"/>

- `Interface options -> VNC -> enable`
- `Display options -> VNC Resolition -> (max) 1920x1080`
- may need to reboot the RPI through the SSH screen `sudo reboot`

### 5.2 Install VNC viewer on client (Windows, MAC OS)
- download: https://www.realvnc.com/en/connect/download/viewer/
- enter IP address of RPI 
<img src="https://github.com/pchat-imm/rpi3/assets/40858099/1860931d-45c8-4d74-8c62-1b61a7504a9b" width="45%" height="45%"/> 

- when enter the screen, enter username and password. `username: chatchamon, password = 12345678'
- The incomplete network won't show the top tap (including Wi-Fi, Bluetooth, and Battery display) 
<img src="https://github.com/pchat-imm/rpi3/assets/40858099/395a5cf1-d1ae-46ef-aa22-e15bbe3e1898" width="45%" height="45%"/>

- the correct RPI interface will include the top tab
    - can see IP address by hovering above the Wi-Fi icon, or see on VNC program
    - see VNC setup 
<img src="https://github.com/pchat-imm/rpi3/assets/40858099/e98cee5a-3cc5-48c9-95f1-d955f7317832" width="45%" height="45%"/>


## 6. add Wi-Fi to RPI<a name = RPIWiFIWPA></a>
- change wpa_supplicant.conf file
```
chatchamon@raspberrypi:~ $ sudo cat /etc/wpa_supplicant/wpa_supplicant.conf 
```
- inside the wpa_supplicant.conf file
```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=TH

network={
 ssid="<WiFi name>"
 psk="<WiFi password>"
 key_mgmt=WPA-PSK

 ssid=”<ssid name>”
 proto=RSN
 key_mgmt=WPA-EAP
 auth_alg=LEAP
 pairwise=CCMP
 group=CCMP
 eap=PEAP
 identity=”<EMPLOYER-ID> -> “your username”
 password=”PASSPHRASE” -> “your password”
 phase2=”auth=MSCHAPV2"
}
```
- (optional) Make the file only readable by root to protect sensitive information.
```
chmod 0600 /etc/wpa_supplicant/wpa_supplicant.conf
```
- Apply new config to the WLAN interface. — or else reboot the system
```
wpa_cli -i wlan0 reconfigure
```

## 7. Use case 1: Quectel<a name = rpi-quectel></a>
![rpi-rpi_quectel](https://github.com/pchat-imm/rpi3/assets/40858099/99c22b8f-624c-4fc1-b2d1-575dd8af914f)
- make RPI connect to internet via 4G/5G using Quectel board. The end result is to be able to ping with 4G/5G using `AT command`, or `wwan0 interface`, or `VNC to the RPI` 
- see Quectel setup info at the repository: https://github.com/pchat-imm/quectel_rm510q_gl 

- see if the RPI can detect hardware connected
```
>> lsusb
Bus 001 Device 005: ID 2c7c:0800 Quectel Wireless Solutions Co., Ltd. RM510Q-GL
Bus 001 Device 004: ID 0424:7800 Microchip Technology, Inc. (formerly SMSC) 
Bus 001 Device 003: ID 0424:2514 Microchip Technology, Inc. (formerly SMSC) USB 2.0 Hub
Bus 001 Device 002: ID 0424:2514 Microchip Technology, Inc. (formerly SMSC) USB 2.0 Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```
- see if there have driver of the quectel hardware
```
>> lsusb -t
        |__ Port 1: Dev 3, If 0, Class=Hub, Driver=hub/3p, 480M
            |__ Port 1: Dev 4, If 0, Class=Vendor Specific Class, Driver=lan78xx, 480M
            |__ Port 3: Dev 5, If 0, Class=Vendor Specific Class, Driver=option, 480M
            |__ Port 3: Dev 5, If 1, Class=Vendor Specific Class, Driver=option, 480M
            |__ Port 3: Dev 5, If 2, Class=Vendor Specific Class, Driver=option, 480M
            |__ Port 3: Dev 5, If 3, Class=Vendor Specific Class, Driver=option, 480M
            |__ Port 3: Dev 5, If 4, Class=Vendor Specific Class, Driver=qmi_wwan, 480M
```
- get operating mode
```
>> sudo qmicli -d /dev/cdc-wdm0 --dms-get-operating-mode 
[/dev/cdc-wdm0] Operating mode retrieved:
	Mode: 'online'
	HW restricted: 'no'
```
- configure network interface
```
>> sudo ip link set wwan0 down
>> echo 'Y' | sudo tee /sys/class/net/wwan0/qmi/raw_ip
>> sudo ip link set wwan0 up
```
- check modem
```
>> sudo mmcli -L
    /org/freedesktop/ModemManager1/Modem/2 [Quectel] RM510Q-GL
```
- see modem info (check on `Status` section to see if it is already connect to the internet, and see the `Hardware` to check the interface)
```
>> sudo mmcli -m 2
```
- then enable the modem
```
>> sudo mmcli -m 2 -e
```
- then connect to the internet
```
>> sudo qmicli -p -d /dev/cdc-wdm0 --device-open-net='net-raw-ip|net-no-qos-header' --wds-start-network="apn='internet',username='true',password='true'" --client-no-release-cid
```
- as the sim is commercial, we need to config it through AT command at minicom
```
>> sudo minicom -s
```
- and set the `Serial Ports Setup`, to have `Serial Device: /dev/ttyUSB2`, and `Hardware Flow Control: No`
- then `save as dfl`, before `exit`
- at minicom, use AT command
```
## check current network selection (7 is LTE, 13 is 5G)
AT+COPS
+COPS: 0,0,"TRUE-H TRUE-H",13
+COPS: 0,0,"TRUE-H TRUE-H",7  

## Firmware update
AT+QMBNCFG=”Select”,”Row_commercial”
OK

## set RAT to LTE & 5G NR
AT+QNWPREFCFG="mode_pref",LTE:NR5G 	
```
- then reboot the quectel board
```
at+cfun=1,1
OK
RDY
+CPIN: READY
+QUSIM: 1
+CFUN: 1
+QIND: SMS DONE
+QIND: PB DONE
TATE0
OK
OK
OK
+CRSM: 148,8,""
OK
+CEMODE: 2
OK
+QGPS: (1-4),(1-255),(1-3),(100-65535)
OK
+CPMS: "ME",18,127,"ME",18,127,"ME",18,127
OK
+CTZU: (0,1)
OK
+CCLK: "24/01/18,08:58:19+28"
OK
RM510QGLAAR11A03M4G                                                             
OK                                                                              
RM510QGLAAR11A03M4G_01.001.01.001                                               
OK 
```
- activate PDP context and PDP address
```
AT+CGACT=1,1
+CCLK: "24/01/18,08:39:27+28"                                                     OK

AT+CGPADDR=1                                                                    
+CGPADDR: 1,"10.101.133.178" 
OK  
```
- verify network setting
```
AT+CGDCONT?
```
### 7.1 ping to see the RPI that connect to Quectel can connect to the internet via 4G/5G
1. try ping to see if it can connect to the internet
```
at+qping=1,"8.8.8.8"                                               
OK                                          
+QPING: 0,"8.8.8.8",32,78,255
+QPING: 0,"8.8.8.8",32,30,255
+QPING: 0,"8.8.8.8",32,44,255
+QPING: 0,"8.8.8.8",32,51,255
+QPING: 0,4,4,0,30,78,50
```
2. then exit minicom, and you can try ping again with `wwan0` interface
```
>> ping -I wwan0 -c 5 8.8.8.8
```
3. You may be able to ping in VNC screen that access the RPI
<img src="https://github.com/pchat-imm/rpi3/assets/40858099/b929e263-4e73-4994-a75c-ce410f8847ba" width="45%" height="45%"/>
