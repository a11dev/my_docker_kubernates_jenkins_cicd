windows wsl
#install docker
### remove old docker installation
sudo apt-get remove docker docker-engine docker.io containerd runc
### update repository
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg lsb-release
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
### setup repository
echo  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
### install docker
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
sudo service docker start
### set up docker user group
sudo groupadd docker
sudo usermod -aG docker personal
#install minikube
curl -LO https://storage.googleapis.com/minikube/releases+/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
### start minikube
minikube start
# install kubectl
### download kubectl e validation
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
curl -LO "https://dl.k8s.io/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
### install kubectl
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
### check installation
kubectl version --client --output=yaml    
kubectl version --client


#start docker
sudo service docker start
# start minikube
minikube start
### create a kubernates jenkins namespace
kubectl create namespace jenkins
kubectl get namespaces
