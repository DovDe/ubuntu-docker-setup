# ubuntu-docker-setup
This repository describes the scripts to setup a ubuntu docker kubernetes system


## Install and setup docker

### setup docker repository
```
sudo apt-get update  
```
```
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```
```
 curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
 ```
 
 ```
 echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
 ```
 
 ### setup docker engine
 
 ```
 sudo apt-get update
 sudo apt-get install docker-ce docker-ce-cli containerd.io
 ```
 
 currently the docker version is:
 *5:20.10.8~3-0~ubuntu-focal*  
 to get updated versions
 *```apt-cache madison docker-ce```*
 ```
 sudo apt-get install docker-ce=5:20.10.8~3-0~ubuntu-focal docker-ce-cli=5:20.10.8~3-0~ubuntu-focal containerd.io
 ```
 
 ## Enable non-root docker use
 
 ```
 sudo apt-get install -y dbus-user-session
 ```
 
 ```
  sudo sh -eux <<EOF
# Install newuidmap & newgidmap binaries
apt-get install -y uidmap
EOF
 ```
 
 ```
 sudo systemctl disable --now docker.service docker.socket
 ```
 
 ```
 dockerd-rootless-setuptool.sh install
 ```
 
 ```
 export PATH=/usr/bin:$PATH
 export DOCKER_HOST=unix:///run/user/1000/docker.sock
 ```
 
 ```
 sudo apt-get install -y docker-ce-rootless-extras
 ```
 
 ## Instal microk8s with snap 
 
 - If snap is not installed install snap
 ```
sudo apt install snapd
 ```
 - install microk8s
```
sudo snap install microk8s --classic
```
- add user to the microk8s group
```
sudo usermod -a -G microk8s <user>
sudo chown -f -R <user> ~/.kube
```
- setup alias for kubectl command
```
echo "alias kubectl='microk8s.kubectl'" >> ~/.bashrc
```

  

 
 
## Terraform Installation
This is taken diectly from the HashiCorp documentation

Update the system
 ```
 sudo apt-get update && sudo apt-get install -y gnupg software-properties-common curl
 ```
 
 
 Add the HashiCorp GPGKey
```
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
```
 
 Add the official HashiCorp Linux repository
 ```
 sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
 ```
 
 Update to add the repository, and install the Terraform CLI
 ```
 sudo apt-get update && sudo apt-get install terraform
 ```
 
 
 
 
 
 
 
 
 
 
