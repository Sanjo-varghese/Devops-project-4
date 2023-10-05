### Jenkins server setup with Helm to deploy into Kubernetes cluster

sudo su -
su - jenkins

## Download and Install helm 
```sh
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```

## On Eks management cluster  copy the config file to jenkins server
navigate to -> Eks management cluster
```sh
cd .kube/
ls -ltr
cat config
```
- copy All the config  file to  jenkins server
Navigate to -> Jenkins server
```sh
sudo su -
su - jenkins
mkdir .kube
cd .kube/
vi config
```
- Paste eks maangement config file to jenkns server config file

## Test with helm command
```sh
helm version
helm list
```

## Copy config file from EKS Management host to Jenkins home directory
```sh
mkdir /var/lib/jenkins/.kube
copy config file under .kube directory with jenkins ownership
```
