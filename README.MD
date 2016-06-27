# Official Docker Image for the University of New Hampshire's programs in Data Science
<img src="EmblemDigital_RGB.png" height=200>

[![DockerPulls](https://img.shields.io/docker/pulls/alexandercbooth/unh.svg)](https://registry.hub.docker.com/u/alexandercbooth/unh/)
## What's inside
- Python 3 w/ data science packages & Jupyter kernel
- R with data science packages & Jupyter kernel
- RStudio
- Scala
- Caravel
- Spark 1.6 with Jupyter Toree kernel for scala
- SQLite3
- Usual linux tools like git and vim
- Docker
- nodejs


## Getting Started

### Docker Toolbox

If you have Docker Toolbox, you will have to first create a virtual machine. The UNH Docker image will run on top of this.

We will setup a virtual machine called unh_vm that has 10Gb of storage, 3 Gb of ram and uses 2 CPU's.

To create, run the following:
```
docker-machine create -d virtualbox --virtualbox-disk-size "10000" --virtualbox-cpu-count "2" --virtualbox-memory "4000" unh_vm
```

Now once this is built, it will automatically be started. In the future, you will have to start it manually with `docker-machine start unh_vm`.

Once the virtual machine is running, we need to make sure docker is connected to it. To do this, run:

```
eval $(docker-machine env unh_vm)
```
Note, you will have to do this every time you start the virtual machine. If you get errors about not being connected to the docker daemon, running the above command should resolve it.

### UNH Docker Image

The following assumes you either have Docker running natively or have started up a vm with docker-machine. If not, see above.

First, we must pull the image from docker hub (Docker's cloud). This is a one time thing -- once you've pulled it the first time, it is now downloaded locally to your computer.

To pull (download), run:
```
docker pull alexandercbooth/unh
```
This should take about 3-5 minutes depending on your internet connection.


To use, simply launch the container like this:
```
docker run -it -p 8888:8888 -v $(pwd):/home/unh/work alexandercbooth/unh
```

Note that `-v $(pwd):/home/unh/work` will mount your current directory to the file system in the container, and the `-p 8888:8888` will map port 8888 in the container to port 8888 on your computer.


A notebook server can then be launched in the usual manner:
```
jupyter notebook --no-browser
```
Then simply visit `http://localhost:8888` in your favorite browser if you're running docker natively. If you are running it on a virtual machine like the one created above, first run `docker-machine ip unh_vm`. This will return the IP of the virtual machine you are running. Now, navigate to `http://IP:8888` where "IP" is the aforementioned IP address.

Similarly, you can run your R, Python and Spark programs from the command line or interactively through their repls.
