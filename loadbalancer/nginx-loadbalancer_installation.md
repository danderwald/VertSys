# Start the nginx loadbalancer

Es wurde eine virtuelle Maschine in der Microsoft Azure Cloud installiert.
Docker musste wieder nach entsprechender Anleitung installiert werden und man startet den loadbalancer mit flogendem Befehl.

```bash
docker run -d -p 80:80 -e WEB_1_PORT_8000_TCP_ADDR=46.101.97.202 -e WEB_2_PORT_8000_TCP_ADDR=46.101.167.186 -e WEB_REMOTE_PORT=8000 -e WEB_PATH=/ -e WEB_BALANCING_TYPE=ip_hash jasonwyatt/nginx-loadbalancer
```


Aus den parametern wird die ```proxy.conf``` in diesem Ordner erstellt.

```-p 80:80``` Port 80 wird an Maschine weitergeleitet
```-e WEB_BALANCING_TYPE=ip_hash``` Balancing wird nach ip_hash Verfahren durchgeführt.
```-e WEB_X_PORT_8000_TCP_ADDR=$IP``` die Hostst auf die verteilt werden soll

