**Creating a Container for Installing Influx DB on Proxmox**

Step 1 - Go to your proxmox server and login

Step 2 - Go to your server local storage > CT templates > Templates

![Downlaoding template for container](https://github.com/Mrhudson69/influxdb-proxmox/assets/78916631/d50238b6-7a17-4112-b2da-6cf966b8f459)

Step 3 - Search for Ubuntu or debian according to your requirement

![Debian or Ubuntu template](https://github.com/Mrhudson69/influxdb-proxmox/assets/78916631/c8780c12-36c6-4a4c-b825-2fb6fcb9347b)

Step 4 - Right click on the server and create a container >> Fill up the basics details and start the container I know you can do it EZ PZ boiss

![Creating Container](https://github.com/Mrhudson69/influxdb-proxmox/assets/78916631/94523447-85b3-49f1-a4f9-3a3a737f559b)

Step 5 - Okay let's create a container 

![image](https://github.com/Mrhudson69/influxdb-proxmox/assets/78916631/485ad835-aba0-4fd6-988b-ac756e06a310)
![image](https://github.com/Mrhudson69/influxdb-proxmox/assets/78916631/c4d494f1-1523-42f8-9a2a-c78fb4df5dc7)
![image](https://github.com/Mrhudson69/influxdb-proxmox/assets/78916631/002e9f00-e69c-41a1-878f-e89606d64831)
![image](https://github.com/Mrhudson69/influxdb-proxmox/assets/78916631/db4ba40d-56df-401d-a74a-a838277df7c4)
![image](https://github.com/Mrhudson69/influxdb-proxmox/assets/78916631/a88bb155-5827-4384-bc5c-2887f45ff014)
![image](https://github.com/Mrhudson69/influxdb-proxmox/assets/78916631/6282b9a3-f42a-4108-a3c9-8dc2b3976caa)

> Now start the container yourself I am not going to teach you that

**Steps to Install InfluxDB V1 (No GUI)**

```
apt update -y

apt install -y influxdb influxdb-client

nano /etc/influxdb/influxdb.conf 
```
add basic configuration in metric server influxDB

```
[[udp]]
   enabled = true 
   bind-address = "0.0.0.0:8089"
   database = "proxmox"
   batch-size = 1000
   batch-timeout = "1s"
```


```
systemctl restart influxdb

systemctl enable influxdb

influx
```

> Show databases

You Will see your databases here

> Exit

**Steps to Install InfluxDB V2 (GUI Acess)**

Go to InfluxDB Download page - https://portal.influxdata.com/downloads/

Login with root 


```
apt update -y

apt install wget

apt install gpg -y

wget -q https://repos.influxdata.com/influxdata-archive_compat.key

echo '393e8779c89ac8d958f81f942f9ad7fb82a25e133faddaf92e15b16e6ac9ce4c influxdata-archive_compat.key' | sha256sum -c && cat influxdata-archive_compat.key | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/influxdata-archive_compat.gpg > /dev/null

echo 'deb [signed-by=/etc/apt/trusted.gpg.d/influxdata-archive_compat.gpg] https://repos.influxdata.com/debian stable main' | sudo tee /etc/apt/sources.list.d/influxdata.list

sudo apt-get update && sudo apt-get install influxdb2

sudo service influxdb start

sudo install ufw

sudo ufw enable

sudo ufw allow 8086

```

```
sudo ufw reload

```
**Pass arguments to systemd**

Add one or more lines like the following containing arguments for influxd to 
```
nano /etc/default/influxdb2
```
add these lines accordingly

```
ARG1="--http-bind-address 0.0.0.0:8087"
ARG2="<another argument here>"
```

Edit the /lib/systemd/system/influxdb.service file as follows

```
nano /lib/systemd/system/influxdb.service
```

Add the below line 

```
ExecStart=/usr/bin/influxd $ARG1 $ARG2
```

```
systemctl daemon-reload

systemctl restart influxdb

systemctl status influxdb
```

**Wolaah Done**

Now You can acess InfluxDB Main interface by going your VM machine IP and port 

```
192.168.13.148:8086
```

![image](https://github.com/Mrhudson69/influxdb-proxmox/assets/78916631/4cad9c9a-5db2-4729-b04c-af70bfa6efbd)








   
