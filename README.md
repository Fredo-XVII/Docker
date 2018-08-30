# Docker
anything docker

# Commands:

  - Got me ssh into the default docker machine: docker-machine -D ssh default 
  - ctrl+C: stop containers and other actions
  - Run container: winpty docker container run -it --rm -p 5000:5000 -e FLASK_APP=app.py -d web1
  - Run container w/ restart on fail w/ port load balancing:
  - winpty docker container run -it -p 5000 -e FLASK_APP=app.py -d --restart on-failure web1
  - Stats: docker container stats
  - Stop container: docker container stop web1


### Install on Windows 10 home, with no Hyper-V
docker-machine create default --virtualbox-no-vtx-check

### For Windows Enterprise - need to set Switch
https://docs.docker.com/docker-for-windows/troubleshoot/#networking-and-wifi-problems-upon-docker-for-windows-install
https://docs.docker.com/machine/drivers/hyper-v/#2-set-up-a-new-external-network-switch-optional

Kilmatic Notes:

If you click on the "exec" icon on the top of the container in Kilmatice it will open a powershell window that will allow you to "cd" into the spark directory and run pyspark.
