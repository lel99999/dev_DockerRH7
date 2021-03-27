# dev_DockerRH7
Docker Integration with RHEL 7.x

#### Specific Aspects of Docker
- PID namespace: Process identifiers and capabilities
- UTS namespace: Host and domain name
- MNT namespace: File system access and structure
- IPC namespace: Process communications over shared memory
- NET namespace: Network access and structure
- USR namespace: User names and identifiers
- chroot(): Controls the location of the file system root
- cgroups: Resource protection

#### Install on RHEL 7 (RedHat Default)
````
$sudo subscription-manager repos --enable=rhel-7-server-rpms
$sudo subscription-manager repos --enable=rhel-7-server-extras-rpms
$sudo subscription-manager repos --enable=rhel-7-server-optional-rpms

$sudo yum install docker device-mapper-libs device-mapper-event-libs
$sudo systemctl start docker.service
$sudo systemctl enable docker.service

$sudo systemctl status docker.service
````


#### Install Docker CE
```
$sudo subscription-manager register --username <username> --password <password> --auto-attach

$sudo subscription-manager repos --enable=rhel-7-server-rpms --enable=rhel-7-server-extras-rpms --enable=rhel-7-server-optional-rpms

$sudo yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
$sudo yum install -y yum-utils device-mapper-persistent-data lvm2
$sudo yum-config-manager --add-repo https://download.docker.com/linux/rhel/docker-ce.repo  
###------- NOTE----------
# edit /etc/yum.repos.d/docker-ce.repo
# CHANGE:
# baseurl=https://download.docker.com/linux/rhel/7/$basearch/stable
# To:
# baseurl=https://download.docker.com/linux/centos/7/x86_64/stable

$sudo yum install docker-ce docker-ce-cli containerd.io

$sudo systemctl enable --now docker.service

$sudo yum list docker-ce --showduplicates | sort -r
```
#### Create docker group and add user
```
$sudo groupadd docker
$sudo usermod -aG docker ${USER}
```

#### Test Docker
```
$docker run hello-world

# https://hub.docker.com/r/nricklin/ubuntu-gpu-test
# Pull down the GPU test image:
$sudo docker pull nricklin/ubuntu-gpu-test

# Run the test:
$DOCKER_NVIDIA_DEVICES="--device /dev/nvidia0:/dev/nvidia0 --device /dev/nvidiactl:/dev/nvidiactl --device /dev/nvidia-uvm:/dev/nvidia-uvm"
sudo docker run $DOCKER_NVIDIA_DEVICES nricklin/ubuntu-gpu-test
```
#### Install Docker Compose
# https://docs.docker.com/compose/install/

```
$sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

$sudo chmod +x /usr/local/bin/docker-compose

$sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose


```


#### TODO:
- [x] 1) Create custom docker base image of RHEL7 <br/>
- [x]    1a) Create a full image using tar <br/>
         1a.1) Download [https://github.com/docker/docker/blob/master/contrib/mkimage-yum.sh](https://github.com/docker/docker/blob/master/contrib/mkimage-yum.sh) <br/>
         1a.2) Edit file and comment 2 lines, then add following line: <br/>
         
         #tar –numeric-owner -c -C “$target” . | docker import - $name:$version <br/>
             
         #docker run -i -t $name:$version echo success <br/>
             
         tar -czvf <filename>.tar.gz /<path_to_image> <br/>
             
- [x]    1b) Create a simple parent image using scratch <br/>
         1b.1) Type following command to import image: <br/> 
         $cat rhel7.9_docker.tar.gz | sudo docker import - UserID/rhel7.9 <br/>
- [x]    1c) Push image to hub.docker.io <br/>
         clouddod/rhel7.9 <br/>
- [ ]    1c1) Type following command to list local images: <br/>
         $docker image ls <br/>
         1c2) Type the following command to push to docker hub: <br/>
         $docker image push REPOSITORY_NAME <br/>
- [ ]    1d) Adding base image to Dockerfile using FROM command followed by base image name:<br/>

```
   # Filename: Dockerfile
   FROM node:test-alpha
```<br/>

2) Copy source code and Wire up internal app to test
  2a) instruct Docker to copy source code during Docker build:
  


10) Add to Docker registry - perhaps Docker hub

#### INFO:
This is a CLI for use with OpenFaaS - a serverless functions framework for Docker & Kubernetes.<br/>
![https://github.com/openfaas/faas-cli](https://github.com/openfaas/faas-cli)

#### Using with Xeon PHI
![https://www.intel.com/content/dam/www/public/us/en/documents/white-papers/running-docker-containers-xeon-phi-whitepaper.pdf](https://www.intel.com/content/dam/www/public/us/en/documents/white-papers/running-docker-containers-xeon-phi-whitepaper.pdf)

#### RHEL 7 Repos for Devtoolset-7
```rhel-server-rhscl-7-rpms
$sudo /usr/bin/subscription-manager repos --enable=rhel-server-rhscl-7-rpms
$sudo yum install devtoolset-7
```

#### Add lessons learned using NVIDIA Docker

#### Add lessons learned using Docker using Intel MIC(Many Integrated Core) architecture with Xeon Phi 

