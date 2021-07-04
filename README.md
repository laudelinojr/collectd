# Instalação do Collect  :cloud:

### OSM Release: 8.0 e 9.0
[OSM](https://osm.etsi.org/docs/user-guide/01-quickstart.html)

## Requisitos mínimos de hardware
- 2 processadores
- 8 Gb de RAM
- 60 Gb disco

## Sistema Operacional
- Ubuntu18.04 (64-bit variant required)

## Passo a Passo para instalação
Serão citadas as instações da versão 8 com docker e versão 9 com kubernetes

## Versão 8 com docker por padrão

1) Sugiro criar na instalaçao do Ubuntu o usuário chamado mano.

2) Execute os comandos abaixo
```bash
sudo groupadd docker
sudo usermod -aG docker mano
newgrp docker
su - mano
```

3) Para instalar o OSM
```bash
wget https://osm-download.etsi.org/ftp/osm-8.0-eight/install_osm.sh
chmod +x install_osm.sh
./install_osm.sh 2>&1 | tee osm_install_log.txt
```

26) Fonte Descriptor autoscaling
https://osm.etsi.org/docs/user-guide/05-osm-usage.html#scaling-descriptor
