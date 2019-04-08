# Install SQL Server Big Data Cluster
## Install Big Data Cluster Tool
```bash
# Install Python3 and pip3
yum install python-pip gcc zlib zlib-devel libffi-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel -y

wget https://www.python.org/ftp/python/3.7.3/Python-3.7.3.tgz
tar -zxvf Python-3.7.3.tgz
cd Python-3.7.3
./configure
make&&make install

# Install MSSQLCTL
pip3 install -r  https://private-repo.microsoft.com/python/ctp-2.4/mssqlctl/requirements.txt --user
```
## Install SQL BDC
```bash
vi .bash_profile
export MSSQLCTL_PATH="/root/.local/bin"
export ACCEPT_EULA="yes"
export CLUSTER_PLATFORM="kubernetes" # kubernetes/ aks/ minikube
export CONTROLLER_USERNAME="???????" # SQL BDC Controller User Name
export CONTROLLER_PASSWORD="???????" # SQL BDC Controller Password
export KNOX_PASSWORD="???????" # Knox Password
export MSSQL_SA_PASSWORD="???????" # SQL Server SA Password
export USE_PERSISTENT_VOLUME=false # NON Presistent Volume for DEMO, If restart cluster then data loss.
export DOCKER_REGISTRY="private-repo.microsoft.com"
export DOCKER_REPOSITORY="mssql-private-preview"
export DOCKER_USERNAME="???????" # EAP Provide
export DOCKER_PASSWORD="???????" # EAP Provide
export DOCKER_EMAIL="???????@microsoft.com" # EAP Provide
export DOCKER_PRIVATE_REGISTRY="?" # EAP Provide
export PATH=$PATH:$MSSQLCTL_PATH

source .bash_profile

mssqlctl cluster create --name sqldemo24
```
![](.\graphics\98.png)<br/>
![](.\graphics\99.png)