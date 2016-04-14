# Galera Load Balancer
## Installation

- git clone https://github.com/codership/glb
- $ cd glb/
- $ ./bootstrap.sh
- $ ./configure
- $ make
- $ sudo make install

## Diensteinrichtung
- cp glbd.sh /etc/init.d/glb

- cp glbd.cfg /etc/default/glbd.cfg (auf debian)


## Konfiguraiton der glbd.cfg in /etc/default/glbd.cfg

LISTEN_ADDR="3306"
DEFAULT_TARGETS="10.128.0.2 10.128.0.3 10.128.0.4"
