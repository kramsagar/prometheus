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


Step4: copy binaries to /usr/local/bin

[root@localhost prometheus-2.47.2.linux-amd64]# cp prometheus /usr/local/bin/
[root@localhost prometheus-2.47.2.linux-amd64]# cp promtool /usr/local/bin/
[root@localhost prometheus-2.47.2.linux-amd64]# chown prometheus:prometheus /usr/local/bin/prometheus
[root@localhost prometheus-2.47.2.linux-amd64]# chown prometheus:prometheus /usr/local/bin/prometheus
[root@localhost prometheus-2.47.2.linux-amd64]#

Step5: copy dashboard related config and folders to /etc/prometheus folder

[root@localhost prometheus-2.47.2.linux-amd64]# cp -r consoles/ /etc/prometheus/
[root@localhost prometheus-2.47.2.linux-amd64]# cp -r console_libraries/ /etc/prometheus/
[root@localhost prometheus-2.47.2.linux-amd64]#

[root@localhost prometheus-2.47.2.linux-amd64]# chown -R prometheus:prometheus /etc/prometheus/consoles/
[root@localhost prometheus-2.47.2.linux-amd64]# chown -R prometheus:prometheus /etc/prometheus/console_libraries/
[root@localhost prometheus-2.47.2.linux-amd64]#

[root@localhost prometheus-2.47.2.linux-amd64]# cp prometheus.yml /etc/prometheus/
[root@localhost prometheus-2.47.2.linux-amd64]# chown prometheus:prometheus /etc/prometheus/prometheus.yml
[root@localhost prometheus-2.47.2.linux-amd64]#


Step6:  overall with current setup so far, we can run prometheus as below:
[root@localhost prometheus-2.47.2.linux-amd64]# 
sudo -u prometheus /usr/local/bin/prometheus    
      --config.file /etc/prometheus/prometheus.yml       
      --storage.tsdb.path /var/lib/prometheus/        
      --web.console.templates=/etc/prometheus/consoles        
      --web.console.libraries=/etc/prometheus/console_libraries

but let us setup a service instead of manally starting with this command:

[root@localhost system]# pwd
/etc/systemd/system

[root@localhost system]# cat prometheus.service
[Unit]
Description=Prometheus Server
Documentation=https://prometheus.io/docs/introduction/overview/
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Restart=on-failure
ExecStart=/usr/local/bin/prometheus  --config.file /etc/prometheus/prometheus.yml --storage.tsdb.path /var/lib/prometheus  --web.console.templates=/etc/prometheus/consoles --web.console.libraries=/etc/prometheus/console_libraries

[Install]
WantedBy=multi-user.target

[root@localhost system]# systemctl daemon-reload

[root@localhost system]# systemctl start prometheus

[root@localhost system]# systemctl status prometheus
● prometheus.service - Prometheus Server
     Loaded: loaded (/etc/systemd/system/prometheus.service; disabled; vendor preset: disabled)
     Active: active (running) since Mon 2023-11-13 13:49:40 IST; 3s ago
       Docs: https://prometheus.io/docs/introduction/overview/
   Main PID: 2777 (prometheus)
      Tasks: 8 (limit: 10972)
     Memory: 21.7M
        CPU: 94ms
     CGroup: /system.slice/prometheus.service
             └─2777 /usr/local/bin/prometheus --config.file /etc/prometheus/prometheus.yml --storage.tsdb.path /var/lib/prometheus --web.console.templates=/etc/promethe>

Nov 13 13:49:40 localhost.localdomain prometheus[2777]: ts=2023-11-13T08:19:40.626Z caller=head.go:760 level=info component=tsdb msg="WAL segment loaded" segment=1 maxS>
Nov 13 13:49:40 localhost.localdomain prometheus[2777]: ts=2023-11-13T08:19:40.626Z caller=head.go:760 level=info component=tsdb msg="WAL segment loaded" segment=2 maxS>
Nov 13 13:49:40 localhost.localdomain prometheus[2777]: ts=2023-11-13T08:19:40.627Z caller=head.go:760 level=info component=tsdb msg="WAL segment loaded" segment=3 maxS>
Nov 13 13:49:40 localhost.localdomain prometheus[2777]: ts=2023-11-13T08:19:40.627Z caller=head.go:797 level=info component=tsdb msg="WAL replay completed" checkpoint_r>
Nov 13 13:49:40 localhost.localdomain prometheus[2777]: ts=2023-11-13T08:19:40.630Z caller=main.go:1045 level=info fs_type=XFS_SUPER_MAGIC
Nov 13 13:49:40 localhost.localdomain prometheus[2777]: ts=2023-11-13T08:19:40.631Z caller=main.go:1048 level=info msg="TSDB started"
Nov 13 13:49:40 localhost.localdomain prometheus[2777]: ts=2023-11-13T08:19:40.631Z caller=main.go:1229 level=info msg="Loading configuration file" filename=/etc/promet>
Nov 13 13:49:40 localhost.localdomain prometheus[2777]: ts=2023-11-13T08:19:40.632Z caller=main.go:1266 level=info msg="Completed loading of configuration file" filenam>
Nov 13 13:49:40 localhost.localdomain prometheus[2777]: ts=2023-11-13T08:19:40.632Z caller=main.go:1009 level=info msg="Server is ready to receive web requests."
Nov 13 13:49:40 localhost.localdomain prometheus[2777]: ts=2023-11-13T08:19:40.633Z caller=manager.go:1009 level=info component="rule manager" msg="Starting rule manage>
lines 1-21/21 (END)
^C
[root@localhost system]# ^C


Try access now: http://192.168.1.14:9090/graph?g0.expr=up&g0.tab=1&g0.stacked=0&g0.show_exemplars=0&g0.range_input=1h









