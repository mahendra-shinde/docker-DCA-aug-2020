Networking (15%)
172. What is the default network that the docker creates automatically?
Bridge
173. How to list the networks on the Docker machine?
docker netwrok ls
174. How to connect to the default bridge network when you create a container?
// since no network is specified, it will be connected to default bridge networkdocker run -dit --name alpine1 alpine ash
175. How to inspect the default network bridge?
docker network inspect bridge
176. The default bridge network is not recommended for production. Is this statement correct?
Yes
177. How to create a user-defined network?
docker network create --driver bridge my-network
178. How to inspect the user-defined network?
docker network inspect my-network
179. How to connect to the user-defined network while creating a container?
docker run -dit --name alpine1 --network my-network alpine ash
180. How to connect the existing container to the user-defined network?
docker netwrok connect my-network alpine2
181. How to troubleshoot a user-defined network?
// using  nicolaka/netshoot
docker run -it --rm --network container:<container_name> nicolaka/netshoot
182. How to publish a port so that it can be accessed externally?
docker run -p 127.0.0.1:$HOSTPORT:$CONTAINERPORT --name CONTAINER -t <image>
183. How to list port mappings or a specific mapping for the container?
// List the containers
docker ps// use this command with container name
docker port <CONTAINER NAME>// USE the specific port
docker port <CONTAINER NAME> <specific port>
184. What are all the different built-in network drivers?
Bridge Network Driver
Overlay Network Driver
MACVLAN Driver
Host
None
185. What are the Bridge network and its use case?
The bridge driver creates a private network internal to the host so containers on this network can communicate.The bridge driver does the service discovery for us automatically if two containers are on the same networkThe bridge driver is a local scope driver, which means it only provides service discovery, IPAM, and connectivity on a single host.
186. What is the scope of the bridge network?
local
187. What are the Overlay network and their use case?
The built-in Docker overlay network driver radically simplifies many of the complexities in multi-host networking.It is a swarm scope driver, which means that it operates across an entire Swarm or UCP cluster rather than individual hosts.
188. What is the scope of the overlay network?
swarm
189. What are the MACVLAN network and their use case?
The macvlan driver is the newest built-in network driver and offers several unique characteristics. It’s a very lightweight driver, because rather than using any Linux bridging or port mapping, it connects container interfaces directly to host interfaces.
190. What is the scope of the macvlan network?
local
191. What are the Host network and its use case?
With the host driver, a container uses the networking stack of the host. There is no namespace separation, and all interfaces on the host can be used directly by the container.
192. What is the scope of the host network?
local
193. What are the None network and its use case?
The none driver gives a container its own networking stack and network namespace but does not configure interfaces inside the container. Without additional configuration, the container is completely isolated from the host networking stack.
194. What is the scope of the None network?
local
195. The Docker networking architecture is built on a set of interfaces called the Container Networking Model (CNM). Is this statement correct?
Yes
196. What is a sandbox in the CNM model?
A Sandbox contains the configuration of a container's network stack. This includes the management of the container's interfaces, routing table, and DNS settings. An implementation of a Sandbox could be a Windows HNS or Linux Network Namespace, a FreeBSD Jail, or other similar concept. A Sandbox may contain many endpoints from multiple networks.
197. What is an endpoint in the CNM model?
An Endpoint joins a Sandbox to a Network. The Endpoint construct exists so the actual connection to the network can be abstracted away from the application. This helps maintain portability so that a service can use different types of network drivers without being concerned with how it's connected to that network.
198. What is a network in the CNM model?
The CNM does not specify a Network in terms of the OSI model. An implementation of a Network could be a Linux bridge, a VLAN, etc. A Network is a collection of endpoints that have connectivity between them. Endpoints that are not connected to a network do not have connectivity on a network.
199. What part of the Docker that provides the actual implementation that makes networks work?
Network Drivers
200. What is IPAM drivers?
Docker has a native IP Address Management Driver that provides default subnets or IP addresses for the networks and endpoints if they are not specified.
201. How to configure docker to use external DNS?
edit the /etc/docker/daemon.json{    
   "dns": ["10.0.0.2", "8.8.8.8"]
}restart the docker
sudo systemctl docker restart
202. Which network should handles control and data traffic related to swarm services?
ingress
203. Which network which connects the individual Docker daemon to the other daemons participating in the swarm?
docker_gwbridge
204. What is the default network created when you create a swarm cluster?
ingress
205. How to create a user-defined overlay network for communication among services?
docker network create -d overlay my-overlay
206. How to create an overlay network which can be used by swarm services or standalone containers to communicate with other standalone containers running on other Docker daemons?
create with --attachable flagdocker network create -d overlay --attachable my-attachable-overlay
207. All the swarm management data is encrypted by default. Is this statement correct?
Yes
208. is application data on the swarm encrypted by default?
No
209. How to encrypt application data as well on the swarm?
// use --opt=encrypted
docker network create --opt encrypted --driver overlay --attachable my-attachable-multi-host-network
210. What is the host port publishing mode?
To publish a service’s port directly on the node where it is running, use the mode=host option to the --publish flag.
