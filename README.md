# GCP ACM / ASM Config Controller + Policy Controller setup


## Initial setup of environment variables

Create a config shell script to create all environmnet variables



Note:
* To determine ip address: `curl -4 ifconfig.co`.

## Stand up config controller instance

This step involves creating the network to host the GKE cluster instance of config controller running. This can be improved by not running in Auto mode for network.

```
make cc-vpc
```

```
make cc-config-controller
```

To interact with the private `configcontroller` cluster we will create a jumpbox within GCP. Determine the ip range of the subnet running `configcontroller`

```
gcloud compute networks subnets describe ${CONFIG_CONTROLLER_NETWORK}-vpc \
    --region ${CONFIG_CONTROLLER_LOCATION} \
    --format 'value(ipCidrRange)'
```

Replace that value within `.hack/config-controller/Makefile` command `k8s-admin-vm` as appropriate.

```
gcloud beta compute instances create k8s-admin \
    ...
    --private-network-ip=10.XXX.1.1
    ...
```

To access cluster via cloud shell:

```
AUTHORIZED_SHELL_NETWORK=dig +short myip.opendns.com @resolver1.opendns.com

gcloud container clusters update krmapihost-configcontroller  \
    --enable-master-authorized-networks \
    --master-authorized-networks ${AUTHORIZED_SHELL_NETWORK}/32 \
    --region ${CONFIG_CONTROLLER_LOCATION} \
    --project ${CONFIG_CONTROLLER_PROJECT_ID}
```

Get the Config Controller instance credentials

```
gcloud anthos config controller get-credentials ${CONFIG_CONTROLLER_NAME} \
    --location ${CONFIG_CONTROLLER_LOCATION}
```