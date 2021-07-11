# Instalação do Collect  :cloud:

### collect: 5.9
[collectd](https://www.collectd.org/)

## Requisitos mínimos de hardware
Não aplicável

## Sistema Operacional
- CentOS

## Passo a Passo para instalação
Siga os passos abaixo para a instalação do collect e posterior envio de dados para o gnocchi.

1) yum install python3-collectd-gnocchi.noarch
 
2) yum install python3-collectd

3) touch /opt/collectd/var/log/collectd.log
 
4) pip install collectd-gnocchi

5) instalar liboping:

5.1) wget http://ftp.uem.br/linux/CentOS/8.1.1911/opstools/x86_64/collectd-5/Packages/l/liboping-1.10.0-12.el8.x86_64.rpm

5.2) yum install liboping-1.10.0-12.el8.x86_64.rpm

Obs.: Este plugin não funcionou


6) Edite arquivo de configuração
```
#
# Config file for collectd(1).
# Please read collectd.conf(5) for a list of options.
# http://collectd.org/
#

#Hostname    "localhost"
#FQDNLookup   true
#BaseDir     "/var/lib/collectd"
#PIDFile     "/var/run/collectd.pid"
#PluginDir   "/usr/lib64/collectd"
#TypesDB     "/usr/share/collectd/types.db"

#Interval     10

#MaxReadInterval 86400
#Timeout         2
#ReadThreads     5
#WriteThreads    5

LoadPlugin logfile

<Plugin logfile>
        LogLevel notice
        File "/opt/collectd/var/log/collectd.log"
        Timestamp true
        PrintSeverity true
</Plugin>

#LoadPlugin aggregation
LoadPlugin cpu
#LoadPlugin cpufreq
#LoadPlugin cpusleep
#LoadPlugin df
#LoadPlugin disk

#LoadPlugin interface
#LoadPlugin load
LoadPlugin memory
LoadPlugin ping
LoadPlugin python

#<Plugin exec>
#       Exec "user:group" "/path/to/exec"
#       NotificationExec "user:group" "/path/to/exec"
#</Plugin>

#<Plugin ping>
#  Host "10.xxx.xxx.12"
#</Plugin>

<Plugin python>
  Import "collectd_gnocchi"
  <Module collectd_gnocchi>
    Endpoint "http://10.XXX.XXX.8:8041"
    User admin

    Auth_Mode keystone
    Auth_Url "http://10.XXX.XXX.8:5000/"
    Username admin
    Project_Name admin
    Password keyxxxxxx
    Project_Domain_Name Default
    User_Domain_Name Default
   </Module>
</Plugin>

Include "/etc/collectd.d"

```

7) Para sempre iniciar o serviço

systemctl enable collectd.service

8) Para iniciar o serviço a primeira vez

systemctl start collectd.service

9) Para verificar as métricas criadas pelo collect no gnocchi
source arquivo_openstack.rc

10) Execute os seguintes comandos gnocchi

gnocchi resource list | grep collectd

11) Anote o id do recurso e faça uma busca para visualizar as metricas, como o exemplo abaixo:

gnocchi metric list | grep 62429693-e331-54c8-94c0-4c54982a6e72


Fontes:

https://github.com/gnocchixyz/collectd-gnocchi

https://github.com/collectd/collectd/

https://www.collectd.org/

https://collectd.org/features.shtml

https://gnocchi.xyz/collectd.html

https://dommgifer.gitbook.io/knowledge/openstack/gnocchi-and-collectd

https://github.com/gnocchixyz/collectd-gnocchi

https://wiki.monitoring-fr.org/nagios/integration/collectd

https://noping.cc/

http://ftp.uem.br/linux/CentOS/8.1.1911/opstools/x86_64/collectd-5/Packages/l/liboping-1.10.0-12.el8.x86_64.rpm
