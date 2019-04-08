# Prepare Kubernetes Master Node
```bash
cat > rbac.yaml <<EOF
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRoleBinding
metadata:
  name: default-rbac
subjects:
- kind: ServiceAccount
  name: default
  namespace: default
roleRef:
  kind: ClusterRole
  name: cluster-admin
  apiGroup: rbac.authorization.k8s.io
EOF

kubeadm init --pod-network-cidr=10.244.0.0/16
```


> [init] Using Kubernetes version: v1.14.0<br/>
> [preflight] Running pre-flight checks<br/>
> [preflight] Pulling images required for setting up a Kubernetes cluster<br/>
> [preflight] This might take a minute or two, depending on the speed of your internet connection<br/>
> [preflight] You can also perform this action in beforehand using 'kubeadm config images pull'<br/>
> [kubelet-start] Writing kubelet environment file with flags to file "/var/lib/kubelet/kubeadm-flags.env"<br/>
> [kubelet-start] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"<br/>
> [kubelet-start] Activating the kubelet service<br/>
> ... ...<br/>
> Your Kubernetes control-plane has initialized successfully!<br/>
> <br/>
> To start using your cluster, you need to run the following as a regular user:<br/>
> <br/>
>   <B><font color="#FFBF00">mkdir -p $HOME/.kube<br/>
>   sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config<br/>
>   sudo chown $(id -u):$(id -g) $HOME/.kube/config<br/></font></B>
> <br/>
> You should now deploy a pod network to the cluster.<br/>
> Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:<br/>
>   https://kubernetes.io/docs/concepts/cluster-administration/addons/<br/>
<br/>
> Then you can join any number of worker nodes by running the following on each as root:<br/>
> <br/>
> <B><font color="#FFBF00">kubeadm join 192.168.0.21:6443 --token a0lxkb.6vt6vr0938cri60z \\<br/>
>     --discovery-token-ca-cert-hash sha256:5549f8fc5a521d328ecc1fb239ee60e47e03da7eedab460f942cdf25337b2d1b<br/></font></B>

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

# Enable CNI
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml

# Apply Dashboard Role-Based Access Control
kubectl apply -f rbac.yaml

# kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml
# Apply and Get Kubernetes Dashboard Laster Version
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v1.10.1/src/deploy/recommended/kubernetes-dashboard.yaml

# Configure By Cluster Access Dashboard Services
kubectl create clusterrolebinding kubernetes-dashboard --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard

# Install CentOS GUI Desktop for use local firefox brower access kubernetes dashboard
yum group list
yum -y groupinstall "GNOME Desktop"
systemctl get-default # multi-user.target
# Set Node Startup by GUI Boot
systemctl set-default graphical.target
# Change from text mode to GUI mode
init 5
```