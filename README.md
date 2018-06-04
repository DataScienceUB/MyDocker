# MyDocker: How to build and use a Docker image for Deep Learning development.

## I.	What is Docker
Docker is a manager of container.

Container:
<div align="center">
	<img width="80%" src="container.png" alt="container"</img>
</div>

•	Isolates app from each other

•	Shares the same kernel – kernel shares resources with the host and interacts with the containers

<div align="center">
	<img width="80%" src="dockervsvm.png" alt="container"</img>
</div>

Advantages

•	Quicker to launch (no os to boot)

•	Portability (less dependencies between processed layers)

•	Efficiency

<div align="center">
	<img width="80%" src="overview.png" alt="container"</img>
</div>	
 
## II.	Run a container

1.	Pull an image from Docker hub: docker login then docker pull <image>
2.	Check the image: docker images
3.	Create a container: docker run –it <nom>
4.	Stop the container: docker stop <id container>
5.	Interact with a container with shell: docker run –it <nom container> /bin/bash
6.	Stop the container
7.	Confirm the container has been stop: docker ps –a
8.	Delete the container: docker rm <id container>


## III.	Build your own container
1.	Create a directory

Commands:

|INSTRUCTION | SIGNIFICATION |
|:-----------|:--------------------------------------------|
|FROM |	Set base image|
|LABEL	| Add metadata|
|COPY	| Copy files/directories into the image|
|ENV	| Set environment variable|
|WORKDIR |	Set working directory|
|RUN	| Execute shell commands in a new layer|
|ENTRYPOINT |	Configure container to run as executable|
|CMD	| Provide default for executing container|

Example 

<div align="center">
	<img width="80%" src="code.png" alt="container"</img>
</div>

2.	Add dependencies by creating reauirements.txt
3.	Build your image:    docker build –t <nom> .
4.	Create the container:    docker run <nom>
5.	Upload to docker hub:    docker login then docker push <image>

## IV.	Exercise
1.	Create a directory
2.	Create your Dockerfile in this new directory.

    FROM ubuntu:latest
    RUN apt-get update && apt-get install -y python3 \
        python3-pip
    COPY requirements.txt .

    RUN pip3 install jupyter
    RUN pip3 install -r requirements.txt
    RUN useradd -ms /bin/bash jupyter
    
    USER jupyter
    
    WORKDIR /home/jupyter
    COPY success.txt .
    ENTRYPOINT ["jupyter", "notebook", "--ip=*"]

3.	Create requirements.txt with Tensorflow, Keras.
4.	Create success.txt
5.	Build your image: docker build -t jupyter .
6.	Get your image id: docker images
7.	Create a new container: docker run -it -p 8888:8888 <image_id> /home
8.	Consulte the results on your browser
