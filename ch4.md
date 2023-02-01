# Chapter 4: Managing Container Images
# Chapter 4 - Section 1: Accessing Registeries
## How to configure registries for the podman command?
`/etc/containers/registries.conf`
For secured registries:  
```
[registries.search]
registries = ["registry.access.redhat.com", "quay.io"]
```   
They by default use the port number 5000 if not specified
But for insecured:  
```
[registries.insecure]
registries = ['localhost:5000']
```


## How to access images registries?
1. Using commands
2. Using APIs

## How using commands?
`podman search [OPTIONS] <term>`  
Options are limit, filter, tls-verify, list-tags

## How using Resitry HTTP API?
To list all repositories available in a registry, use the /v2/_catalog endpoint. The n parameter is used to limit the number of repositories to return:
```
curl -Ls https://myserver/v2/_catalog?n=3
{"repositories":["centos/httpd","do180/custom-httpd","hello-openshift"]}
```
If Python is available, use it to format the JSON response:
```
curl -Ls https://myserver/v2/_catalog?n=3 \
| python -m json.tool
```
The /v2/<name>/tags/list endpoint provides the list of tags available for a single image:
```
curl -Ls \
https://quay.io/v2/redhattraining/httpd-parent/tags/list \
| python -m json.tool
```
## Note
Quay.io offers a dedicated API to interact with repositories beyond what is specified in Docker Repository API. See https://docs.quay.io/api/ for details.

## Note
The registry HTTP API requires authentication credentials. First, use the Red Hat Single Sign On (SSO) service to obtain an access token:  
`curl -u username:password -Ls "https://sso.redhat.com/auth/realms/rhcc/protocol/redhat-docker-v2/auth? service=docker-registry"`  

Then, include this token in a Bearer authorization header in subsequent requests:  
