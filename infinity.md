syslinux-tftpboot
httpd
dnsmasq


cp undionly.kpxe /tftpboot

## What's the use of the dhcp?
* To provide temporary IP
## What's the use of the mac?
* To not to interrupt main operation of machines in the network

## How to make pxe allowed in dmz where it's a different subnet, router doesn't allow dhcp broadcast?
* Using dhcp relay, or just manually deploy the dmz machines


Packages for pxeboot
kernel
rootfs
initramfs
+
The ignition file ==> bootstrap.ign
then network configuration:
* IP, gateway,  mask, DNSs, hostname

## How to install the OC commandline?
* Using the compressed file of the OC

## How to create the ignition file?
* Using the compressed file of the `openshift installer` command

## Then activate the auto-completion, from the documentation


pxeboot
download packages
configuration files ===> .ipxe, dnsmasq.d
start services
stop firewall
configure autocompletion





vms specs
which prism
which network
Create manifists
disable worker craetion
Create the ignition files ==> 3 ===> chmod +r

# Notes
* There have to be 3-masters
1. MAsters should start with each other


Monitoring:
* crictl ps
* systemctl status




- 3-storages ===> block/nfs/buckets
- certificate
- LDAP
- LDAP o group


oc get co






# htpasswd for OAuth
# Router pods
# Router pods in the dmz zone's nodes
# nc -u -z ip port
# OC get cluster version








* Day2-operation
1. Move components ===> monitoring/routes/image registry ===> to infra node


- node labeling ==> infra
- taint toleration for the infra node (Scheduler topic)
- monitoring ===> get conf from documenation


2. Create block storage
- Download Nutanix CSI "Container Storage Interface" operator for cluster to integrate with nutanix infra
- Create nfs and secret components (yml and create)
- Edit the  ===> oc edit storageclasses.storage.k8s.io nutanix-dynfiles
- Edit images registry to pull a storage because it won't work without it
- oc edit configs.imageregistry.operator.openshift.io
- oc get pvc -A ===> Bound/Pending

3. Install ACS Operator

4. Install Kasten KIO ===> Backup


5. Create image registry ===> oc create new-app


6. Create from setrix ===> nutanix CSI documentation

7. Create storage class

8. Create cluster logging operator

*


9. Create ACS
* create SecuredCluster ===> stackrox
* Create stackrox and secrets
* Donwload bundle
* Create secured custom resource
* oce get 


1. htpasswd auth
`https://docs.openshift.com/container-platform/4.12/authentication/identity_providers/configuring-htpasswd-identity-provider.html`

2. move routers, monitorying , registry, to infra
3. taint and label
4. confiure cis
5. storage class
https://opendocs.nutanix.com/openshift/operators/csi/
6. change api cert
7. apps cert
8. ldap
9. kastin backup
10. ntp machine config
11. etcd enc
12. health check
13. etcd backup operation
14. subscription



10. Configure ntp using machine config:
- Creating a machine config pool to make sure to hit the infra nodes when hitting worker nodes
- Using MachineConfigSelector

11. Enable iscsi in all nodes


12. Certificates ===> Replacing the default ingress certificate
- API ===> To communicate with the cluster
- Apps


13. Adding api certificate
`https://docs.openshift.com/container-platform/4.12/security/certificates/api-server.html`



14. Encode etcd configuration
`https://docs.openshift.com/container-platform/4.12/security/encrypting-etcd.html`


15. Groups synchronization ===> whitelisting
`ldap-sync-group.yml` ===> kind:ldapsyncConfig
`https://docs.openshift.com/container-platform/4.9/authentication/ldap-syncing.html`

16. Add policies for the groups


17. Moving
`https://access.redhat.com/solutions/5034771`




18. Kasten
* Add kasten profile
* Make sure to add the user to the bucket configuration

## IN DMZ
1. Configure Network
2. Configure hostname
* Validate DNS
3. Installation on any platform `https://docs.openshift.com/container-platform/4.10/installing/installing_platform_agnostic/installing-platform-agnostic.html` ===> Advanced ===> `https://docs.openshift.com/container-platform/4.10/installing/installing_platform_agnostic/installing-platform-agnostic.html#installation-user-infra-machines-advanced_installing-platform-agnostic`




```
journalctl -x -f
curl -vk quay.io
oc whoami -t
```
