# Fleet Example

You need a k8s cluster with Rancher > 2.5 deployed and another cluster registered into Rancher.

## Installation

Fleet is built natively in Rancher since version 2.5.
The clusters you register in Rancher are automatically registered into Rancher Continuous Delivery. 
An agent is deployed on each downstream cluster.

## Examples

First we can create our operator 1 ClusterGroup
```
kubectl apply -f groups/op1-group.yaml
```

Then we can deploy a Bundle to monitor operators/op1/index.yaml, in order to create an index.html configmap for nginx
```
kubectl apply -f operators/op1/config.yaml
```

We can now create a new Bundle to monitor apps/, to deploy our nginx Helm chart for the dev-group ClusterGroup. See nginx/fleet.yaml.
```
kubectl apply -f groups/dev-group.yaml
kubectl apply -f apps/nginx.yaml
```

Now, let's use the release/1.0 branch and deploy a release/1.0 bundle
```
git checkout release/1.0
kubectl apply -f apps/nginx.yaml
```