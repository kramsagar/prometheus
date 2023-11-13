Step1: create a user to operate the prometheus processes and services.

[root@localhost ~]# adduser --no-create-home --shell /bin/false prometheus
[root@localhost ~]#


Step2: 
1. create folder for storing configurations (prometheus.yml)
2. create folder for stroing the tsdb
3. give permissions

[root@localhost ~]# mkdir /etc/prometheus
[root@localhost ~]# mkdir /var/lib/prometheus
[root@localhost ~]# chown prometheus:prometheus /etc/prometheus
[root@localhost ~]# chown prometheus:prometheus /var/lib/prometheus
[root@localhost ~]#


![image](https://github.com/kramsagar/prometheus/assets/130482831/7eae8705-54c6-4a34-bcef-0f983948d4fd)

