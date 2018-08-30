# Docker
anything docker

# Commands:


docker-machine -D ssh default - got me ssh into the default docker machine.
ctrl+C: stop containers and other actions
Run container: winpty docker container run -it --rm -p 5000:5000 -e FLASK_APP=app.py -d web1
Stats: docker container stats


### Install on Windows 10 home, with no Hyper-V
docker-machine create default --virtualbox-no-vtx-check

### For Windows Enterprise - need to set Switch
https://docs.docker.com/docker-for-windows/troubleshoot/#networking-and-wifi-problems-upon-docker-for-windows-install
https://docs.docker.com/machine/drivers/hyper-v/#2-set-up-a-new-external-network-switch-optional

Kilmatic Notes:

If you click on the "exec" icon on the top of the container in Kilmatice it will open a powershell window that will allow you to "cd" into the spark directory and run pyspark.
