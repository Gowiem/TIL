# Creating a K8ns Service that uses a AWS's ELB and serves traffic over HTTPs

Steps:

1. Create the Service: `kube expose deployment mattgowiedotcom --port=443 --target-port=443 --name=mattgowiedotcom --type=LoadBalancer`
2. Annotate the Service so it knows how to properly configure the ELB:
```
kube annotate services SERVICE_NAME service.beta.kubernetes.io/aws-load-balancer-backend-protocol=http
kube annotate services SERVICE_NAME service.beta.kubernetes.io/aws-load-balancer-ssl-cert=AWS_CERT
kube annotate services SERVICE_NAME service.beta.kubernetes.io/aws-load-balancer-ssl-ports='443'
```
