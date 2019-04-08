# Prepare Each Node
## CentOS update & upgrade
```bash
# Update Yum Repo
yum update -y
# Upgrade CentOS Kernel
yum upgrade -y

# IP HOSTNAME
echo $(hostname -i) $(hostname) >> /etc/hosts

# Set SELinux to permissive or disabled and Effective immediately
setenforce 0
sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config

# Set OS Firewall stop and service disable 
systemctl stop firewalld
systemctl disable firewalld

# Install the necessary software 
yum install -y ntp wget net-tools yum-utils device-mapper-persistent-data lvm2

# Manual Synchronization Time
ntpdate -s 0.pool.ntp.org
```
## Docker Installation
```bash
# Download Docker Repo file
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

# Update Repo
yum update -y

# Install Docker
yum install docker-ce docker-ce-cli containerd.io -y

systemctl status docker
# Auto start docker service with OS start
systemctl enable docker
# Start Docker Service immediate
systemctl start docker
# Test Docker running been normal.
docker run hello-world

# Kubernetes 1.14 need: cgroupdriver=systemd
cat > /etc/docker/daemon.json <<EOF
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "100m"
  },
  "storage-driver": "overlay2",
  "storage-opts": [
    "overlay2.override_kernel_check=true"
  ]
}
EOF

mkdir -p /etc/systemd/system/docker.service.d

systemctl daemon-reload
systemctl restart docker

```
## Kubernetes Installation
```bash
# Disable SWAP
sed -i "/ swap / s/^/#/" /etc/fstab
swapoff -a

# Download Kubernetes Repo and Key
cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
exclude=kube*
EOF

# Setting Docker and Kubernetes bridge network
cat <<EOF >  /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF

# Install Kubernetes
yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes

# Auto start kubelet with OS start
systemctl enable kubelet

# Kubernetes Offical Document has some issue
# Issue Script: systemctl enable kubelet && systemctl start kubelet
# systemctl start kubelet # DO NOT EXECUTE
```