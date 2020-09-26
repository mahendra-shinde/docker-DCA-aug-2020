## Installation and Configuration (15%)

123. What is the recommended way of installing Docker
set up docker repositories
install from them for the ease of installation and upgrade tasks.
124. How to upgrade docker-engine?
sudo apt-get update
install docker from the instructions from here
125. How to uninstall docker?
sudo apt-get purge docker-ce
sudo rm -rf /var/lib/docker
126. Are Images, containers, volumes, or customized configuration files on your host are not automatically removed when you uninstall docker?
No. You need to explicitly delete those
127. How to add the user to the Docker group and use docker as a non-root user?
sudo usermod -aG docker your-user
128. What are the ways to install docker?
1. using repositories
2. using DEB package
3. using convience scripts
129. How to install Docker CE on Centos?
// uninstall older versions
sudo yum remove docker \
                docker-client \
                docker-client-latest \
                docker-common \
                docker-latest \
                docker-latest-logrotate \
                docker-logrotate \
                docker-engine// install required libs
sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2// set up the stable repo
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo// install
sudo yum install docker-ce docker-ce-cli containerd.io// if you want to install specific versions
sudo yum install docker-ce-<VERSION_STRING> docker-ce-cli-<VERSION_STRING> containerd.io// start docker
sudo systemctl start docker
130. How to install Docker CE on Debian?
// uninstall older versions
sudo apt-get remove docker docker-engine docker.io containerd runc// update
sudo apt-get update// install required 
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg2 \
    software-properties-common// add dockers official gpg key
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -// set up stable repo
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"// update and install
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io// if you want to install specific versions
sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io
131. How to install Docker CE on Fedora?
// uninstall old versions
sudo dnf remove docker \
                docker-client \
                docker-client-latest \
                docker-common \
                docker-latest \
                docker-latest-logrotate \
                docker-logrotate \
                docker-selinux \
                docker-engine-selinux \
                docker-engine// install required packages
sudo dnf -y install dnf-plugins-core// add the stable repo
sudo dnf config-manager \
    --add-repo \
    https://download.docker.com/linux/fedora/docker-ce.repo// install community version
sudo dnf install docker-ce docker-ce-cli containerd.io// if you want specific versions
sudo dnf -y install docker-ce-<VERSION_STRING> docker-ce-cli-<VERSION_STRING> containerd.io// start docker
sudo systemctl start docker
132. How to install Docker CE on Ubuntu?
// uninstall old versions
sudo apt-get remove docker docker-engine docker.io containerd runc// update and install required packages
sudo apt-get updatesudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common// add official gpg key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -// stable repo
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"// update and install
sudo apt-get updatesudo apt-get install docker-ce docker-ce-cli containerd.io// if you want specific versions
sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io
133. What are the recommended storage drivers on different distributions?
Centos: overlay2
Ubuntu supports overlay2, aufs and btrfs storage drivers. Overlay2 is the default one
134. What are all the release channels that Docker CE supports?
Stable gives you latest releases for general availability.
Test gives pre-releases that are ready for testing before general availability.
Nightly gives you latest builds of work in progress for the next major release.
135. Where are the Docker-CE binaries available?
Docker Engine - Community binaries for a release are available on download.docker.com as packages for the supported operating systems.
136. Where are the Docker-EE binaries available?
Docker Hub
137. What are logging drivers?
Docker has multiple mechanisms to get the logging information from running docker containers and services. These mechanisms are called logging drivers
138. How to configure a logging driver for the Docker daemon so that all the containers use it?
configure log-driver in /etc/docker/daemon.json{
  "log-driver": "syslog"
}
139. Whats is the default logging driver?
json-file
140. If you have configurable options for your logging driver how do you specify?
use log-opts in the daemon.json file{
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "10m",
    "max-file": "3",
    "labels": "production_status",
    "env": "os,customer"
  }
}
141. How to find the logging driver for the Docker daemon?
docker info --format '{{.LoggingDriver}}'
142. How to configure a logging driver for a container?
docker run -it --log-driver json-file --log-opt max-size=10m alpine ash
143. What are the available logging drivers for the Docker CE edition?
json-file
local
journald
144. If the swarm loses the quorum of managers it loses the ability to perform management tasks. Is this statement correct?
Yes
145. If the swarm loses quorum all the existing tasks and services are all deleted. Is this statement correct?
No. All the existing tasks will continue to run. But, new nodes cannot be added and new tasks can't be created.
146. We should use a fixed IP address for the advertise address to prevent the swarm from becoming unstable on machine reboot. Is this statement correct?
Yes. If the whole swarm restarts and every manager node subsequently gets a new IP address, there is no way for any node to contact an existing manager. Therefore the swarm is hung while nodes try to contact one another at their old IP addresses.
147. You should maintain an odd number of managers in the swarm to support manager node failures. Is this statement correct?
Yes.
148. I have manager nodes 3, 5, 7, 9. How do you distribute these manager nodes on availability zones so that If you suffer a failure in any of those zones, the swarm should maintain the quorum of manager nodes
Manager Nodes           Availability Zones    3                     1-1-1
    5                     2-2-1
    7                     3-2-2
    9                     3-3-3
149. How to drain the node
docker node update --availability drain <NODE>
150. How to cleanly rejoin a manager node in the cluster?
1. To demote the node to a worker, run docker node demote <NODE>
2. To remove the node from the swarm, run docker node rm <NODE>
3. Re-join the node to the swarm with a fresh state using docker swarm jo
151. How to forcibly remove a node?
docker node rm --force <NODE>
152. If you want to remove a manager node you need to demote it to a worker role first. Is this statement correct?
Yes. You must ensure that there is a quorum
153. What is the location where swarm managers save the swarm state?
/var/lib/docker/swarm
154. How to backup the swarm?
1. If autolock is enabled. You must unlock the swarm
2. stop the docker on the manager node so that you don't have unpredictable results
3. save the entire contents of /var/lib/docker/swarm
4. start the manager
155. How to restore swarm from the backup?
1. shut down the docker on the targeted machine
2. Remove the contents of /var/lib/docker/swarm
3. Restore the /var/lib/docker/swarm directory from the backup
4. Start the docker on the node so that it doesn't connect to old ones
docker swarm init --force-new-cluster5. Verify the state of the swarm docker service ls
6. rotate the autolock key
7. Add manager and worker nodes for the required capacity
8. backup this swarm
156. What is a team in the DTR?
A team defines the permissions a set of users have for a set of repositories.
157. What are all the permission levels that teams could have?
Read Only: View repository and pull images.
Read Write: View repository, pull and push images.
Admin: Manage repository and change its settings, pull and push images.
158. Where is the Docker daemon directory?
/var/lib/docker on Linux
C:\ProgramData\docker on Windows
159. How to enable the debugging on Docker daemon
1. add this flag in /etc/docker/daemon.json{
  "debug": true
}2. Send a HUP signal to the daemon to cause it to reload its configuration.sudo kill -SIGHUP $(pidof dockerd)
160. How to check whether Docker is running?
// all these can be used depending on the operating system
docker infosudo systemctl is-active docker
sudo status docker
sudo service docker status
161. What are the hardware and software requirements for UCP?
Minimum
1. 8GB of RAM for manager nodes or nodes running DTR
2. 4GB of RAM for worker nodes
3. 3GB of free disk spaceRecommended
1. 16GB of RAM for manager nodes or nodes running DTR
2. 4 vCPUs for manager nodes or nodes running DTR
3. 25-100GB of free disk space
162. What products that Docker EE contains?
UCP
DTR
Docker Engine with enterprise-grade support,
163. Where is the location of the custom certificates?
/etc/docker/certs.d
164. What are the ports that DTR uses?
80/tcp     -     Web app and API client access to DTR.
443/tcp    -     Web app and API client access to DTR
165. DTR needs to be installed on a worker node that is being managed by UCP. You can't install DTR on a standalone Docker engine. Is this statement correct?
Yes
166. How to backup the UCP
To create a UCP backup, run the docker/ucp:2.2.22 backup command on a single UCP managerdocker container run \
  --log-driver none --rm \
  --interactive \
  --name ucp \
  -v /var/run/docker.sock:/var/run/docker.sock \
  docker/ucp:2.2.22 backup \
  --id <ucp-instance-id> \
  --passphrase "secret" > /tmp/backup.tar
167. How to restore the UCP
docker/ucp:2.2.22 restore --passphrase "secret"docker container run --rm -i --name ucp \
  -v /var/run/docker.sock:/var/run/docker.sock  \
  docker/ucp:2.2.22 restore --passphrase "secret" < /tmp/backup.tar
168. You need to backup the UCP on the single manager node since Docker maintains the same UCP state in all the manager nodes. Is this statement correct?
Yes
169. How to backup the DTR?
To perform a backup of a DTR node, run the docker/dtr backup command.
170. DTR requires that a majority (n/2 + 1) of its replicas are healthy at all times for it to work. So if a majority of replicas are unhealthy or lost, the only way to restore DTR to a working state is by recovering from a backup. Is this statement correct?
Yes
171. How to configure Docker to start on boot?
sudo systemctl enable docker
