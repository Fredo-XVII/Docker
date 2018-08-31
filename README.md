# Docker
anything docker

# Commands:
  
  ## Build Images:
  - Got me ssh into the default docker machine: docker-machine -D ssh default 
  - docker image build -t web1 .
  
  ## Containers:
  
  - ctrl+C: stop containers and other actions
  - Run container: winpty docker container run -it --rm -p 5000:5000 -e FLASK_APP=app.py -d web1
  - Run container w/ restart on fail w/ port load balancing:
  - winpty docker container run -it -p 5000 -e FLASK_APP=app.py -d --restart on-failure web1
  - Stats: docker container stats
  - Stop container: docker container stop web1
  
  ## Volumes:
  -  UNIX volumes: winpty docker container run -it -p 5000:5000 -e FLASK_APP=app.py --rm --name web1 -e FLASK_DEBUG=1 -v $PWD:/app web1
  -  PC volumes: winpty docker container run -it -p 5000:5000 -e FLASK_APP=app.py --rm --name web1 -e FLASK_DEBUG=1 -v "C:\Users\Z001C9V\OneDrive - Target Corporation\Documents\GitHub\Docker\Dive_Into_Docker\src\06-docker-in-the-real-world\03-creating-a-dockerfile-part-1":/app web1
  
  ## Debugging:
  - connect to running container: winpty docker container exec -it web1 bash
    - exec: puts you in the root directoy of the docker container (now you use linux commands to navigate)
      - linux commands:
        - rm *.pyc
   - setting users for volume files: winpty docker container exec -it --user "$(id -u):$(id -g)" web1 touch hi.txt


### Install on Windows 10 home, with no Hyper-V
docker-machine create default --virtualbox-no-vtx-check

### For Windows Enterprise - need to set Switch
https://docs.docker.com/docker-for-windows/troubleshoot/#networking-and-wifi-problems-upon-docker-for-windows-install
https://docs.docker.com/machine/drivers/hyper-v/#2-set-up-a-new-external-network-switch-optional

Kilmatic Notes:

If you click on the "exec" icon on the top of the container in Kilmatice it will open a powershell window that will allow you to "cd" into the spark directory and run pyspark.
