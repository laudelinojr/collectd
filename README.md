# Instalação do Collect  :cloud:

### collect: 5.9
[collectd](https://www.collectd.org/)

## Requisitos mínimos de hardware
Não aplicável

## Sistema Operacional
##Ubuntu18.04 (64-bit variant required)
- CentOS

## Passo a Passo para instalação
Siga os passos abaixo para a instalação do collect e posterior envio de dados para o gnocchi.

1) Sugiro criar na instalaçao do Ubuntu o usuário chamado mano.



yum install python3-collectd-gnocchi.noarch

yum install python3-collectd

touch /opt/collectd/var/log/collectd.log

#pip install collectd ( a confirmar)

pip install collectd-gnocchi

instalar liboping


2) Edite arquivo de configuração
```bashssssss
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
