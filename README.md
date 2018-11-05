# Docker
  - Docker set up on Centos: https://docs.docker.com/install/linux/docker-ce/centos/

# Set up and install:

  ### Install on Windows 10 home, with no Hyper-V
  docker-machine create default --virtualbox-no-vtx-check

  ### For Windows Enterprise - need to set Switch
  https://docs.docker.com/docker-for-windows/troubleshoot/#networking-and-wifi-problems-upon-docker-for-windows-install
  https://docs.docker.com/machine/drivers/hyper-v/#2-set-up-a-new-external-network-switch-optional


# Commands:
  
  ## Build Images:
  - Got me ssh into the default docker machine: docker-machine -D ssh default 
  - docker image build -t web1 .
  
  ## Containers:
  
  - ctrl+C: stop containers and other actions
  - Run container: winpty docker container run -it --rm -p 5000:5000 -e FLASK_APP=app.py -d web1
  - Run container w/ restart on fail w/ port load balancing:
  - winpty docker container run -it -p 5000 -e FLASK_APP=app.py -d --restart on-failure web1
  - winpty docker container run -it --rm -p 3838:3838 --name sisterstore sisterstore, or,
   - winpty docker container run -it -p 3838:3838 --name sisterstore --restart on-failure sisterstore
  - Stats: docker container stats
  - Stop container: docker container stop web1
  
  ## Volumes:
  -  UNIX volumes: winpty docker container run -it -p 5000:5000 -e FLASK_APP=app.py --rm --name web1 -e FLASK_DEBUG=1 -v $PWD:/app web1
  -  PC volumes: winpty docker container run -it -p 5000:5000 -e FLASK_APP=app.py --rm --name web1 -e FLASK_DEBUG=1 -v "C:\Users\Z001C9V\OneDrive - Target Corporation\Documents\GitHub\Docker\Dive_Into_Docker\src\06-docker-in-the-real-world\03-creating-a-dockerfile-part-1":/app web1
  - Volume code below is working:
  - winpty docker container run -it -p 3838:3838 --name sisterstore -v "C:/Users/Z001C9V/Target/OneDrive_Data/OneDrive - Target Corporation/Documents/GitHub/ShinyApps/SISTER_STORE_SELECTOR/app_logs/":/var/log/shiny-server/ --restart on-failure sisterstore
  - NAMED VOLUMES - great for databases or when you need to share data
    - command: docker volume create <name> -> ENTER
    - command: docker volume ls
    - command: docker volume inspect <name of named volume>
    
  ## Debugging:
  -  Interactive in Docker Container: 
    - connect to running container: 
      - winpty docker container exec -it <name of container> sh 
      - winpty docker container exec -it web1 bash
    - exec: puts you in the root directoy of the docker container (now you use linux commands to navigate)
      - linux commands:
        - rm *.pyc
   - setting users for volume files: winpty docker container exec -it --user "$(id -u):$(id -g)" web1 touch hi.txt

  ### Using interpreter:
  - Interactive R: winpty docker container run -it --rm --name testingR r-base:latest R
  - 

  ## Connecting Containers over Network:
  - VOLUME ["path inside container"]command - expose file in the Docker file and container
    - or, add "-v /app/dir" to expose the path when you first run the container.
  - --volume-from <name of container w/exposed volume path>
  
  ## CMD instruction: 
  - CMD passes code to an ENTRYPOINT script
  - default shell instruction: /bin/sh -c "code"
  
  ## Cleaning Up:
  - docker container ls : go to command to see what containers are running
  - docker container ls -a : show containers that have been stopped as well.
  - docker system df : how much disk space docker is using.
    - docker system df -v : more details listed
  - docker images ls : dangling images...images with the <none> tag are dangling safe to delete
  - docker system info : gives docker install info
  - docker system prune : will delete all excess stuff from docker.
    - docker system prune -f : skips confirmation (yes/no) so great for cron job...no human input.
    - - docker system prune -a : deletes images with no running containers...can be dangerous...think before running
  - docker container stop $(docker container ls -a - q) : stops all running containers.
 
# Docker COMPOSE
  - HELP: docker -compose --help
  - docker-compose build - build the image
  - docker-compose pull - pull dependencies of the imgage
  - docker-compose up - run the compose image.
  - SHORT CUT: docker-compose up --build -d
  - docker-compose ps
  - LOGS: docker-compose logs -f # for when you are in -d mode and you want to see the logs. CTRL + C to exit.
  - RESTART: docker-compose restart < container name if you want just one container >
  - BASH commands to container: docker-compose exec web(name of container) ls -la
    - INTERACTIVE prompt: docker-compose exec web sh
  - docker-compose run redis(container_name) redis-server --version
  
-----

# Kilmatic Notes:

If you click on the "exec" icon on the top of the container in Kilmatice it will open a powershell window that will allow you to "cd" into the spark directory and run pyspark.

# Resources
  - file:///C:/Users/Z001C9V/Downloads/CERN_openlab_Nitin_Agarwal.pdf
  - https://www.cloudandheat.com/blog/docker-containers-on-openstack-vms-2/
  - http://goinbigdata.com/docker-run-vs-cmd-vs-entrypoint/
  - **AMAZING RESOURCE** - https://www.symbolix.com.au/blog-main/r-docker-hello
  - **rocker/shiny** - https://github.com/rocker-org/rocker-versioned/blob/master/rstudio/README.md
  - **BASH CMD** - https://www.codeguru.com/csharp/csharp/cs_internet/using-r-with-docker-engine.html#Item4
  - **containerit package:** https://o2r.info/2017/05/30/containerit-package/
  - **install.r/installGithub.r** - https://cran.r-project.org/web/packages/littler/vignettes/littler-examples.html
  - **Remove sudo requirement** - https://docs.docker.com/install/linux/linux-postinstall/#manage-docker-as-a-non-root-user
  - **Remove TTY requirement** - https://www.shell-tips.com/2014/09/08/sudo-sorry-you-must-have-a-tty-to-run-sudo/
    - make sure to remove the -t when using docker image build: https://stackoverflow.com/questions/43099116/error-the-input-device-is-not-a-tty
  - **Docker Build Reference**: https://docs.docker.com/engine/reference/commandline/build/#options
