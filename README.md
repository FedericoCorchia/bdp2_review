# BDP2 Review
Midterm Review exercise for the BDP2 Course, University of Bologna.

This exercise tests the following:
- extension of a basic Jupyter Notebook Docker image with the addition of the Redis module so that it comes already installed in the extended Jupyter image;
- automatical build of the extended image and its publication on DockerHub;
- build of an application stack, running the extended Jupyter image, Redis and Portainer through Docker Compose.

To launch the extended Jupyter image produced in this exercise and published on DockerHub enter:

```docker run -d --rm --name my_jupyter -v ~/review/bdp2_review/work:/home/jovyan -p 80:8888 --network bdp2-net -e JUPYTER_ENABLE_LAB=yes -e JUPYTER_TOKEN="<CHOOSE_A_PASSWORD>" --user root -e CHOWN_HOME=yes -e CHOWN_HOME_OPTS="-R" federicocorchia/extended-notebook```
