What is DCT?
Through DCT, image publishers can sign their images and image consumers can ensure that the images they use are signed.
212. What is DCT stand for?
Docker Content Trust
213. What is the command to generate delegation keys?
docker trust generate key
214. How to load if you have any existing keys?
docker trust key load
215. How to sign a particular tag and push it up to the registry?
docker trust sign dtr.example.com/admin/demo:1
216. How to enable docker content trust so that you can sign images automatically when you use docker push?
export DOKCER_CONTENT_TRUST=1
217. How to inspect remote trusted data for a tag?
docker trust inspect
218. How to remove remote trusted data for a tag?
docker trust revoke
219. What is a grant?
A grant defines who has how much access to set of resources
220. What is the subject?
A subject can be user, team, organization and is granted a role for set of resources
221. What is the role?
A role is a set of permitted API operations that you can assign to a specific subject and collection by using a grant
222. What is a Client Bundle?
A client bundle is a group of certificates downloadable directly from the Docker Universal Control Plane (UCP) user interface within the admin section for “My Profile”. This allows you to authorize a remote Docker engine to a specific user account managed in Docker EE, absorbing all associated RBAC controls in the process. You can now execute docker swarm commands from your remote machine that take effect on the remote cluster.
223. What is the easiest way to access or control the UCP?
Client Bundle
224. What is the kernel feature that isolates the processes running in different containers?
Namespaces
225. Which kernel feature limits the resources used by docker containers?
Control Groups
226. What is the kernel feature that needed extra configuration?
user
227. Docker swarm should be secure by default?
yes
________________________________________
Storage and Volumes (10%)
228. What is the pluggable architecture that Docker supports for the container writable layer storage?
Storage Drivers
229. What is the preferred storage driver for all Linux distributions which need no extra configuration?
Overlay2
230. Which device-mapper driver is used for production environments?
direct-lvm
231. Which device-mapper driver is used for testing environments?
loopback-lvm
232. How do you check the current storage driver information?
docker info
233. How do you configure device-mapper?
// stop docker
sudo systemctl stop docker// set the device-mapper in /etc/docker/daemon.json file
{
  "storage-driver": "devicemapper"
}//start docker
sudo systemctl start docker
234. what is the option that sets the direct-lvm for production device-mapper?
dm.directlvm_device
235. What do you set the device-mapper and all configurable options in the daemon.json?
{
  "storage-driver": "devicemapper",
  "storage-opts": [
    "dm.directlvm_device=/dev/xdf",
    "dm.thinp_percent=95",
    "dm.thinp_metapercent=1",
    "dm.thinp_autoextend_threshold=80",
    "dm.thinp_autoextend_percent=20",
    "dm.directlvm_device_force=false"
  ]
}
236. What are the different available storage options available for containers?
Block Storage
FiLE System Storage
Object Storage
237. Do containers create a writable layer on top of Image read-only layers?
Yes
238. Where is the Docker’s local storage area?
/var/lib/docker/<storage-driver>
239. What is the difference between bind mounts and volumes?
Volumes are completely managed by docker
Bind Mounts are dependent on the host directory structure
240. Volumes don’t increase the size of the containers. Is this statement correct and why?
Yes. Because volumes live outside of containers
241. What should we use if we want to persist the data beyond the lifecycle of the containers?
Volumes
242. How to create a Volume?
docker volume create my-volume
243. How to list docker volumes?
docker volume ls
244. How to inspect docker volume?
docker volume inspect my-vol
245. How to remove docker volumes?
docker volume rm my-vol
246. If you start a container with a volume that does not yet exist, Docker creates the volume for you. Is this statement correct?
Yes
247. How to create a volume myvol2 with a docker run?
docker run -d \
  --name devtest \
  -v myvol2:/app \
  nginx:latest
248. How to verify the volume is created with the container?
// Look for the mounts section
docker inspect devtest
249. How to create a volume with the --mount flag?
docker run -d \
  --name devtest \
  --mount source=myvol2,target=/app \
  nginx:latest
250. How to remove all unused images not just dangling images?
docker system prune --all

