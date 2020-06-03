# pulsar_docker
Builds a docker image for a pulsar analysis packages and few extras on Ubuntu 18.04 LTS. Forked from https://github.com/mserylak/pulsar_docker

You'll find all pulsar software in /home/psr/software, environment variables are set according to ~/.mysetenv.bash file.

To build:

    docker build -t vivek_pulsar_docker .
    
Alternatively, you can pull the latest build from docker hub as:

    docker pull vivekvenkris/vivek_pulsar_docker:latest

# USE in Docker:

If you have built it manually, you can use the following instructions as-is. If you have pulled it from docker hub, please replace `vivek_pulsar_docker` with `vivekvenkris/vivek_pulsar_docker` everywhere. 

To run image in docker:

    docker run -it vivek_pulsar_docker /bin/bash 

To mount data directory into the docker container with the -v flag:

    docker run -it -v <data_location on host>:/data vivek_pulsar_docker /bin/bash

This will drop you in to an ubuntu os with bash shell with all data in /data.

To run the image with X11 and mounted data directory, run the container first:

    docker run -d -p 2222:22 -v <data_location on host>:/data vivek_pulsar_docker

Check if container is running with docker ps -a. You can log in using **psr** as password:

    ssh -XY psr@localhost -p 2222

# USE in Singularity:

To use the docker image in singularity, you probably need to change the CACHE and TMP dirs that Singularity uses or you will get a ```NO SPACE LEFT ON DEVICE``` error. Set the following environment variables to a directory of your choice. 

    export SINGULARITY_LOCALCACHEDIR=/fpra/mkat/01/users/vivek
    export SINGULARITY_CACHEDIR=/fpra/mkat/01/users/vivek
    export SINGULARITY_TMPDIR=/fpra/mkat/01/users/vivek

    singularity shell -B <host_directory> docker://vivekvenkris/vivek_pulsar_docker:latest

# Issues
Report problems to vkrishnan@mpifr-bonn.mpg.de
