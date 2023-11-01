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





   
