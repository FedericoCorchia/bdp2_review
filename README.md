# BDP2 Review
Midterm Review exercise for the BDP2 Course, University of Bologna. It extends a Docker image and pushes it to DockerHub.

Launch the image with:

```docker run -d --rm --name my_jupyter -v ~/review/bdp2_review/work:/home/jovyan -p 80:8888 --network bdp2-net -e JUPYTER_ENABLE_LAB=yes -e JUPYTER_TOKEN="<CHOOSE_A_PASSWORD>" --user root -e CHOWN_HOME=yes -e CHOWN_HOME_OPTS="-R" federicocorchia/extended-notebook```
