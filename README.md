# BDP2 Review
Midterm Review exercise for the BDP2 Course, University of Bologna.

This exercise tests the following:
- extension of a basic Jupyter Notebook Docker image with the addition of the Redis module so that it comes already installed in the extended Jupyter image;
- automatic build of the extended image and its publication on DockerHub;
- build of an application stack, running the extended Jupyter image, Redis and Portainer through Docker Compose.

## 1. Extension of Jupyter Image
The aim of this exercise is to extend image ```minimal-notebook``` (DockerHub: ```jupyter/minimal-notebook```) so that it already comes with Redis installed. This is done through the Dockerfile at ```docker/Dockerfile```.

## 2. Automatic Build of the Extended Image and Publication on DockerHub
The aim of this exercise is to have the Jupyter extended image automatically built and published on DockerHub at every ```git push``` command. This is done by the GitHub action at ```.github/workflows/docker-image.yml```. The image gets published on DockerHub at https://hub.docker.com/repository/docker/federicocorchia/extended-notebook.

The extended image published on DockerHub can then be launched with:

```docker run -d --rm --name my_jupyter -v ~/review/bdp2_review/work:/home/jovyan -p 80:8888 --network bdp2-net -e JUPYTER_ENABLE_LAB=yes -e JUPYTER_TOKEN="<CHOOSE_A_PASSWORD>" --user root -e CHOWN_HOME=yes -e CHOWN_HOME_OPTS="-R" federicocorchia/extended-notebook```

followed by the Redis image launch command:

```docker run -d --rm --name my_redis -v ~/review/bdp2_review/work:/data --network bdp2-net --user 1000 redis redis-server```

The extended image has been tested by creating a Jupyter notebook running basic Python and Redis commands. The notebook, at ```work/Redis_on_Extended_Notebook.ipynb```, runs as expected. Redis file ```dump.rdb``` is also created as expected in folder ```work``` (then renamed on this repository as ```dump_CREATED_BY_extended-notebook.rdb``` to make sure it is correctly created also by the Docker-Compose stack later on).

## 3. Docker Compose Application Stack Running Jupyter, Redis and Portainer
The aim of this exercise is to build an application stack running the extended Jupyter image, Redis and Portainer through Docker Compose. The Docker Compose script is ```docker-compose.yml``` in the top folder.

The test done in Part 2 has also been performed on this stack, either with network ```bdp2-net``` already created prior to the starting of the stack (notebook ```work/Redis_on_Extended_Notebook+Docker_Compose_And_bdp2-net.ipynb```) or without it (notebook ```work/Redis_on_Extended_Notebook+Docker_Compose_Without_bdp2-net.ipynb```). Redis file ```dump.rdb``` is again correctly created (again renamed on this repository as ```work/dump_CREATED_BY_extended-notebook+Docker_Compose_And_bdp2-net.rdb``` and ```work/dump_CREATED_BY_extended-notebook+Docker_Compose_Without_bdp2-net.rdb``` respectively, so that the absence of a file called exactly ```work/dump.rdb``` forces its recreation under all considered testing conditions - extended image on its own, Docker Compose stack with prior bdp2-net, Docker Compose stack without prior bdp2-net).

