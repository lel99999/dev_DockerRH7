# dev_DockerRH7
Docker Integration with RHEL 7.x

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
