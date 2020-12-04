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

#### TODO:
1) Create docker base image of RHEL7<br/>
  1a) Create a full image using tar

  1b) Create a simple parent image using scratch


  1e) Adding base image to Dockerfile using FROM command followed by base image name:<br/>
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
