---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
1. install UTM: https://mac.getutm.app/
2. download ubuntu server iso: https://ubuntu.com/download/server/arm
3. open utm, select iso, boot it
4. install ubuntu via text interface
5. `sudo apt install ubuntu-desktop`
6. `systemctl enable gdm3`
	1. will ask for your password a bunch of times and end with a warning
7. `systemctl start gdm3`
	1. should bring up the login page