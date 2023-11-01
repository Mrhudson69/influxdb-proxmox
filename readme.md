**Creating a Container for Installing Influx DB on Proxmox**

Step 1 - Go to your proxmox server and login

Step 2 - Go to your server local storage > CT templates > Templates

![Downlaoding template for container](https://github.com/Mrhudson69/influxdb-proxmox/assets/78916631/d50238b6-7a17-4112-b2da-6cf966b8f459)

Step 3 - Search for Ubuntu or debian according to your requirement

![Debian or Ubuntu template](https://github.com/Mrhudson69/influxdb-proxmox/assets/78916631/c8780c12-36c6-4a4c-b825-2fb6fcb9347b)

Step 4 - Right click on the server and create a container >> Fill up the basics details and start the container I know you can do it EZ PZ boiss

![Creating Container](https://github.com/Mrhudson69/influxdb-proxmox/assets/78916631/94523447-85b3-49f1-a4f9-3a3a737f559b)

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





   
