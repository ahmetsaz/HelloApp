# HelloApp
- There is a Dockerfile for .net core 3.1 in the application.
- I used github action for the Docker file CI process. You can check the action.yml file in the .github/workflows/ file. I sent the generated image in ahmetsaz/helloapp.

 To run the Docker Image:

  - docker pull ahmetsaz/helloapp:latest
  - docker run -p 11130:11130 ahmetsaz/helloapp:latest

- I used Azure for Kubernetes cluster environment(Azure Kubernetes Service)
- I used ansible to create the Azure kubernetes service. You can check the aks_ansible.yml file. If you want to delete the resource, you can check the aks_ansible_destroy.yml file.
- To use the aks ansible.yml file, you need to login azure with az login. Then you need to create a service principal with az name sp create-for-rbac --name ServicePrincipalName.
- az name sp create-for-rbac --name ServicePrincipalName command output:
```javascript
{
  "appId": "myAppId",
  "displayName": "myDisplayName",
  "name": "http://myName",
  "password": null,
  "tenant": "myTenantId"
}
```
- Edit the aks_ansible.yml file according to the service principal output:

```javascript
{
    resource_group: Rg-k8s
    location: westeurope
    aks_name: pt-cluster
    username: azureuser
    ssh_key: "your ssh key"
    client_id: "your appId"
    client_secret: "your password"
    aks_version: 1.16.10
}
```

To run the Ansbile:
 - ansible-playbook aks_ansible.yml (create aks cluster)
 - ansible-playbook aks_ansible_destroy.yml (destroy aks cluster)
 
For pod auto scale: 
- I used https://github.com/Azure/azure-k8s-metrics-adapter/tree/master/samples/request-per-second
