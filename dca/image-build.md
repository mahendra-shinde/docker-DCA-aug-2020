Image Creation, Management, and Registry (20%)
57. Which instruction sets the base image for the subsequent builds in the Dokcerfile?
FROM
58. No instruction can precede FROM in the Dockerfile. Is this statement correct?
No. ARG is the only instruction can precede FROM
59. What are the two forms for the RUN instruction?
shell form: RUN <command>
exec form: RUN ["executable", "param1", "param2"]
60. What does the RUN instruction do in the Dockerfile?
The RUN instruction will execute any commands in a new layer on top of the current image and commit the results.
61. The RUN command normally utilizes cache from the previous build. Which flag should you specify for the build not to use cache?
--no-cachedocker build --no-cache .
62. Is there any other instruction that can invalidate the cache?
Yes. ADD
63. How many forms that CMD instruction has?
CMD ["executable","param1","param2"] (exec form, this is the preferred form)CMD ["param1","param2"] (as default parameters to ENTRYPOINT)CMD command param1 param2 (shell form)
64. If CMD instruction provides default arguments for the ENTRYPOINT instruction, both should be specified in JSON format. Is this statement correct?
Yes
65. What is the purpose of the CMD instruction in the Dockerfile?
The main purpose of a CMD is to provide defaults for an executing container. These defaults can include an executable, or they can omit the executable, in which case you must specify an ENTRYPOINT instruction as well.
66. How to make your container execute the same executable every time?
use ENTRYPOINT in combination with CMD
67. What is the purpose of the LABEL instruction in the Dockerfile?
It adds metadata to the Image
68. How to check the labels for the current image?
docker inspect // Under Labels section
69. The EXPOSE instruction actually publish the port. Is this statement correct?
No. It serves as a type of documentation between the image publisher and image consumer
70. What should you do to actually publish the ports?
use -p flag when running a container
71. What is the purpose of the ENV instruction in the Dockerfile?
ENV <key> <value>an ENV instruction sets the enviroment value to the key and it is available for the subsequent build steps and in the running container as well.
72. How to change the environment variables when running containers?
docker run --env <key>=<value>
73. What is the difference between ADD and COPY instructions?
ADD [--chown=<user>:<group>] <src>... <dest>The ADD instruction copies new files, directories or remote file URLs from <src> and adds them to the filesystem of the image at the path <dest>.COPY [--chown=<user>:<group>] <src>... <dest>The COPY instruction copies new files or directories from <src> and adds them to the filesystem of the container at the path <dest>.
74. What is ENTRYPOINT instruction in the Dockerfile?
An ENTRYPOINT allows you to configure a container that will run as an executable.Command line arguments to docker run <image> will be appended after all elements in an exec form ENTRYPOINT, and will override all elements specified using CMD.
75. How can you override the ENTRYPOINT instruction?
docker run --entrypoint
76. What is the VOLUME instruction in the Dockerfile?
The VOLUME instruction creates a mount point with the specified name and marks it as holding externally mounted volumes from native host or other containers.
77. What initializes the newly created Volume?
docker run -v
78. What is the USER instruction in the Dockerfile?
The USER instruction sets the user name (or UID) and optionally the user group (or GID) to use when running the image and for any RUN, CMD and ENTRYPOINT instructions that follow it in the Dockerfile.
79. What is the WORKDIR instruction in the Dockerfile?
The WORKDIR instruction sets the working directory for any RUN, CMD, ENTRYPOINT, COPY and ADD instructions that follow it in the Dockerfile.
80. You have specified multiple WORKDIR instructions in the Dockerfile what is the result WORKDIR?
WORKDIR /a
WORKDIR b
WORKDIR c
RUN pwdresult: /a/b/c
81. You have specified multiple WORKDIR instructions in the Dockerfile what is the result WORKDIR?
WORKDIR /a
WORKDIR /b
WORKDIR c
RUN pwdresult: /b/c
82. What is the ARG instruction in the Dockerfile?
ARG <name>[=<default value>]The ARG instruction defines a variable that users can pass at build-time to the builder with the docker build command using the --build-arg <varname>=<value> flag.
83. What is the ONBUILD instruction in the Dockerfile?
The ONBUILD instruction adds to the image a trigger instruction to be executed at a later time, when the image is used as the base for another build.
84. Which instruction sets the system call signal that will be sent to the container to exit?
STOPSIGNAL signal
85. Which instruction let Docker daemon know the health of the container?
HEALTHCHECK
86. What are all the options that can be provided for the HEALTHCHECK instruction?
--interval=DURATION (default: 30s)
--timeout=DURATION (default: 30s)
--start-period=DURATION (default: 0s)
--retries=N (default: 3)
87. What is the SHELL instruction in the Dockerfile?
The SHELL instruction allows the default shell used for the shell form of commands to be overridden. The default shell on Linux is ["/bin/sh", "-c"], and on Windows is ["cmd", "/S", "/C"]. The SHELL instruction must be written in JSON form in a Dockerfile.
88. Create ephemeral containers is considered best practice?
Yes
89. What should you do if you want to exclude some files while executing the docker build image and don’t want to send all the files to Docker daemon?
use .dockerignore file
90. What is the best way to drastically reduce the size of an image?
Multi Stage Builds
91. How do you minimize the number of layers while building the image?
Only the instructions RUN, COPY, ADD create layers.Where possible, use multi-stage builds, and only copy the artifacts you need into the final image.sort multi line arguments
RUN apt-get update && apt-get install -y \
  bzr \
  cvs \
  git \
  mercurial \
  subversion
92. How to leverage the build cache?
Put instructions that likely to change often at the bottom of the dockerfile.
93. How to remove unused images?
docker image prune
94. How to see the history of the image?
docker image history
95. How to format the output of the docker inspect command?
by using --format flag//examples
docker inspect --format='{{range .NetworkSettings.Networks}}{{.MacAddress}}{{end}}' $INSTANCE_IDdocker inspect --format='{{.LogPath}}' $INSTANCE_ID
96. How to tag an image?
docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]docker tag 0e5574283393 fedora/httpd:version1.0 // by id
docker tag httpd fedora/httpd:version1.0 // by name
docker tag httpd:test fedora/httpd:version1.0.test // by name and tagdocker tag 0e5574283393 myregistryhost:5000/fedora/httpd:version1.0
97. How to run a local registry?
docker run -d -p 5000:5000 --restart=always --name registry registry:2
98. How to copy an image from the docker hub to a local repository?
// pull an image from the Docker Hub
docker pull ubuntu// tag an image
docker tag ubuntu:16.04 localhost:5000/my-ubuntu// push the image
docker push localhost:5000/my-ubuntu
99. How to stop and remove a local registry?
docker container stop registry && docker container rm -v registry
100. How to display the layers of the Docker image?
docker image inspect //under Layers section
101. How to create a Docker image from archive or stdin?
docker image load// example
docker image load -i example.tar
102. How to modify an image to a single layer?
// take any multiple layer image
// run the container
docker export <container> > single-layer.tar
docker import /path/to/single-layer.tar
// check the history
docker image history
103. Each layer is only a set of differences from the layer before it. The layers are stacked on top of each other. Is this statement about the image correct?
Yes
104. When you create a container It adds one writable layer on top of all the layers of the image. Is this statement about the image correct?
yes
105. What is the copy-on-write (CoW) strategy?
Copy-on-write is a strategy of sharing and copying files for maximum efficiency. If a file or directory exists in a lower layer within the image, and another layer (including the writable layer) needs read access to it, it just uses the existing file. The first time another layer needs to modify the file (when building the image or running the container), the file is copied into that layer and modified. This minimizes I/O and the size of each of the subsequent layers.
106. How to customize the registry while deploying?
// customize published port
docker run -d \
  -p 5001:5000 \
  --name registry-test \
  registry:2// If you want to change the port the registry listens on within the containerdocker run -d \
  -e REGISTRY_HTTP_ADDR=0.0.0.0:5001 \
  -p 5001:5001 \
  --name registry-test \
  registry:2// storage customization
docker run -d \
  -p 5000:5000 \
  --restart=always \
  --name registry \
  -v /mnt/registry:/var/lib/registry \
  registry:2

107. How to configure a registry?
The Registry configuration is based on a YAML file. you can specify a configuration variable from the environment by passing -e arguments to your docker run stanza or from within a Dockerfile using the ENV instruction.// for example you have a configuration like this for root directory
storage:
  filesystem:
    rootdirectory: /var/lib/registry// you can create environment variable like this
REGISTRY_STORAGE_FILESYSTEM_ROOTDIRECTORY=/somewhereit will change from /var/lib/registry to /somewhere
108. What is the location of the registry configuration file?
/etc/docker/registry/config.yml
109. How to customize an entire config file of registry?
docker run -d -p 5000:5000 --restart=always --name registry \
             -v `pwd`/config.yml:/etc/docker/registry/config.yml \
             registry:2
110. How to login to a self-hosted registry?
docker login localhost:5000
111. Where do you configure any credential helpers or credentials for the registry to prevent passing every time you log in?
/etc/docker/daemon.json
112. How to limit the number of records when docker search?
docker search nginx --limit=2
113. How to format the docker search?
docker search --format "{{.Name}}: {{.StarCount}}" nginx
114. How to disable Image signing while pushing an image to the repository?
docker push [OPTIONS] NAME[:TAG]--disable-content-trust=true
115. How to enable docker content trust in the Docker CLI?
export DOCKER_CONTENT_TRUST=1
docker push <dtr-domain>/<repository>/<image>:<tag>
116. How to pull an image from the repository?
docker pull [OPTIONS] NAME[:TAG|@DIGEST]// pulling from docker hub by default
docker pull debian// pulling from other repositories
docker pull myregistry.local:5000/testing/test-image
117. How to pull an image with multiple images?
-a or --all-tags
docker pull --all-tags fedora
118. How to remove all images which are not used by existing containers?
docker image prune -a
119. How to limit the scope when pruning images?
by uisng --filter flag
docker image prune -a --filter "until=24h"
120. How to remove an image?
docker rmi <IMAGE ID>
121. How to remove image without deleting the untagged parent images?
docker rmi --no-prune <IMAGE ID>
122. How to delete an image from the repository?
login into DTR web UI
go to the TAGS section delete the specific TAG 
you can also delete all images by deleting the entire repository
