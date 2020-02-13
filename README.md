# Kubernetese Basic

### Pre installed tools: awscli, kops, kubectl
Find the installation instructions in below links:
#### AWSCLI: https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html
#### KOPS: https://github.com/kubernetes/kops/blob/master/docs/install.md
#### kubectl: https://kubernetes.io/docs/tasks/tools/install-kubectl/
##### Pro TIP - also configure Autocompletion for best performance
### create env file:
```
cat project.env << EOF
export AWS_ACCESS_KEY_ID=<ACCESS key>
export AWS_SECRET_ACCESS_KEY=<Secret key>
export KOPS_STATE_STORE=s3://<S3 bucket name>
export CLUSTER_NAME=<clustername>.k8s.local
EOF
```
### Execute the file
`
source project.env
`

### Execute KOPS to create a new cluster
`
kops create cluster --zones ap-south-1a $CLUSTER_NAME
`
### edit the config below to modify the zones and region
```
kops edit cluster ${CLUSTER_NAME}  
```
### To edit the node and master configration use the below command. [Optional]
```
kops edit instancegroup  --name $CLUSTER_NAME nodes
kops edit ig --name=$CLUSTER_NAME master-ap-south-1a
```
```
kops update cluster ${CLUSTER_NAME} --yes
```
### A new cluster with 1 master and 2 nodes will be created


```
Cluster is starting.  It should be ready in a few minutes.

Suggestions:
 * validate cluster: kops validate cluster
 * list nodes: kubectl get nodes --show-labels
 * ssh to the master: ssh -i ~/.ssh/id_rsa admin@api.monte-cluster.k8s.local
 * the admin user is specific to Debian. If not using Debian please use the appropriate user based on your OS.
 * read about installing addons at: https://github.com/kubernetes/kops/blob/master/docs/addons.md.
```



### Explore the cluster and name spaces
```
kubectl config get-context
# kubectl config use-context  <Cluster name>

kubectl get pod
kubectl get pod -n kube-system

```



### Apply the manifest files using below commands
```
kubectl apply -f <filename>

kubectl get pod (-n namespace if mentioned explicitly)
kubectl describe pod
#kubectl describe (object name)

kubectl explain deployment #or any object name
kubectl port-forward <podname> <localport>:<container port>

kubectl  get pod -L KEY:VALUE  #The selector query

```
