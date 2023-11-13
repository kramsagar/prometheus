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

Step3:
Download the software
[root@localhost ~]# wget https://github.com/prometheus/prometheus/releases/download/v2.47.2/prometheus-2.47.2.linux-amd64.tar.gz
--2023-11-13 12:04:54--  https://github.com/prometheus/prometheus/releases/download/v2.47.2/prometheus-2.47.2.linux-amd64.tar.gz
Resolving github.com (github.com)... 20.207.73.82
Connecting to github.com (github.com)|20.207.73.82|:443... connected.
HTTP request sent, awaiting response... 302 Found
prometheus-2.47.2.linux-amd64.ta 100%[=========================================================>]  91.27M  25.6MB/s    in 5.0s

2023-11-13 12:05:01 (18.1 MB/s) - ‘prometheus-2.47.2.linux-amd64.tar.gz’ saved [95708924/95708924]

[root@localhost ~]#

[root@localhost ~]# ls -ltr
total 93472
-rw-r--r--. 1 root root 95708924 Oct 12 22:22 prometheus-2.47.2.linux-amd64.tar.gz
-rw-------. 1 root root     1082 Nov  6 22:34 anaconda-ks.cfg

[root@localhost ~]# tar xvf prometheus-2.47.2.linux-amd64.tar.gz
prometheus-2.47.2.linux-amd64/
prometheus-2.47.2.linux-amd64/LICENSE
prometheus-2.47.2.linux-amd64/NOTICE
prometheus-2.47.2.linux-amd64/prometheus.yml
prometheus-2.47.2.linux-amd64/consoles/
prometheus-2.47.2.linux-amd64/consoles/prometheus.html
prometheus-2.47.2.linux-amd64/consoles/prometheus-overview.html
prometheus-2.47.2.linux-amd64/consoles/node-cpu.html
prometheus-2.47.2.linux-amd64/consoles/index.html.example
prometheus-2.47.2.linux-amd64/consoles/node.html
prometheus-2.47.2.linux-amd64/consoles/node-disk.html
prometheus-2.47.2.linux-amd64/consoles/node-overview.html
prometheus-2.47.2.linux-amd64/promtool
prometheus-2.47.2.linux-amd64/console_libraries/
prometheus-2.47.2.linux-amd64/console_libraries/prom.lib
prometheus-2.47.2.linux-amd64/console_libraries/menu.lib
prometheus-2.47.2.linux-amd64/prometheus
[root@localhost ~]#


Step4:



