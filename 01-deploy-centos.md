# CentOS 7 Installation by GUI
## 1. Boot Image
Choose: Install CentOS 7<br/>
![](.\graphics\02.png)
## 2. Language
Choose: Keep default <br/>
![](.\graphics\03.png)
## 3. Date & Time
![](.\graphics\04.png)
Asia -> Shanghai<br/>
![](.\graphics\05.png)
## 4. Installation Destination
Custom Partition:<br/>
SWAP: 8192MB<br/>
BOOT(/boot): 512MB<br/>
ROOT(/): All<br/>
![](.\graphics\06.png)<br/>
![](.\graphics\07.png)<br/>
![](.\graphics\08.png)<br/>
![](.\graphics\09.png)<br/>
![](.\graphics\10.png)
## 5. Disable KDUMP
![](.\graphics\11.png)
## 6. Disable Security Policy
![](.\graphics\12.png)
## 7. Setting Host Name
![](.\graphics\13.png)
## 8. Setting Network
![](.\graphics\14.png)
![](.\graphics\15.png)
## 9. Review Configuration and Begin for Installation
![](.\graphics\16.png)
## 10. Setting password for account root
![](.\graphics\17.png)<br/>
![](.\graphics\18.png)
## 11. Waiting for install, and reboot OS
![](.\graphics\19.png)
## 12. Locally and Remotely Login
![](.\graphics\20.png)<br/>
![](.\graphics\21.png)<br/>
Done!

> P.S. Sample

| ID | Node Name | IP | Mask | Gateway | DNS |
| --- | --- | --- | --- | --- | --- |
| 1 | ck8sn01 | 192.168.0.21 | 24 | 192.168.0.253 | 8.8.8.8 |
| 2 | ck8sn02 | 192.168.0.22 | 24 | 192.168.0.253 | 8.8.8.8 |
| 3 | ck8sn03 | 192.168.0.23 | 24 | 192.168.0.253 | 8.8.8.8 |
| 4 | ck8sn04 | 192.168.0.24 | 24 | 192.168.0.253 | 8.8.8.8 |