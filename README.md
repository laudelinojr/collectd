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


6) Edite arquivo de configuração
```
#
# Config file for collectd(1).
# Please read collectd.conf(5) for a list of options.
# http://collectd.org/
#

##############################################################################
# Global                                                                     #
#----------------------------------------------------------------------------#
# Global settings for the daemon.                                            #
##############################################################################

#Hostname    "localhost"
#FQDNLookup   true
#BaseDir     "/var/lib/collectd"
#PIDFile     "/var/run/collectd.pid"
#PluginDir   "/usr/lib64/collectd"
#TypesDB     "/usr/share/collectd/types.db"


#----------------------------------------------------------------------------#
# Interval at which to query values. This may be overwritten on a per-plugin #
# base by using the 'Interval' option of the LoadPlugin block:               #
#   <LoadPlugin foo>                                                         #
#       Interval 60                                                          #
#   </LoadPlugin>                                                            #
#----------------------------------------------------------------------------#
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

#LoadPlugin write_log
#LoadPlugin write_prometheus


#<Plugin aggregation>
#  <Aggregation>
#    #Host "unspecified"
#    Plugin "cpu"
#    #PluginInstance "unspecified"
#    Type "cpu"
#    #TypeInstance "unspecified"
#
#    GroupBy "Host"
#    GroupBy "TypeInstance"
#
#    CalculateNum false
#    CalculateSum false
#    CalculateAverage true
#    CalculateMinimum false
#    CalculateMaximum false
#    CalculateStddev false
#  </Aggregation>
#</Plugin>

#<Plugin cpu>
#  ReportByCpu true
#  ReportByState true
#  ValuesPercentage false
#  ReportNumCpu false
#  ReportGuestState false
#  SubtractGuestState true
#</Plugin>
#

#<Plugin exec>
#       Exec "user:group" "/path/to/exec"
#       NotificationExec "user:group" "/path/to/exec"
#</Plugin>



#<Plugin memory>
#       ValuesAbsolute true
#       ValuesPercentage false
#</Plugin>

#<Plugin ping>
#  Host "10.159.205.12"
#</Plugin>


#<Plugin python>
#       ModulePath "/path/to/your/python/modules"
#       LogTraces true
#       Interactive true
#       Import "spam"

#       <Module spam>
#               spam "wonderful" "lovely"
#       </Module>
#</Plugin>

<Plugin python>
  Import "collectd_gnocchi"
  <Module collectd_gnocchi>
    Endpoint "http://10.159.205.8:8041"
    User admin

    Auth_Mode keystone
    Auth_Url "http://10.159.205.8:5000/"
    Username admin
    Project_Name admin
    Password keystoneadmin
    Project_Domain_Name Default
    User_Domain_Name Default
   </Module>
</Plugin>

Include "/etc/collectd.d"

```


Fontes:

https://www.collectd.org/

https://collectd.org/features.shtml

https://gnocchi.xyz/collectd.html

https://dommgifer.gitbook.io/knowledge/openstack/gnocchi-and-collectd

https://github.com/gnocchixyz/collectd-gnocchi

https://wiki.monitoring-fr.org/nagios/integration/collectd

https://noping.cc/

http://ftp.uem.br/linux/CentOS/8.1.1911/opstools/x86_64/collectd-5/Packages/l/liboping-1.10.0-12.el8.x86_64.rpm
