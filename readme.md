## Install openshift on Bare metal instance

### Instructions
Please note that this terraform script is designed to used with CloudShell on your Oracle Cloud Account.
And make sure that you have enough privileges to create resources or manage tenancy before executing this script. 
You should have your own Domain and Point to the Name Servers provided at the end of the Terraform script execution.

This installer designed to work with https://console.redhat.com/openshift assisted cluster installation method. 

### Steps to be followed
1. Clone/Download this repository to your CloudShell (Will update orahub url later. Please use attached zip for the moment)
2. Generate OpenSSH key pairs using ssh-keygen if you do not have it already on your CloudShell environment
3. signup for redhat account
4. Go to Assisted Cluster Creation Wizard on RedHat OpenShift Conole and copy live ISO download command after providing your ssh public key
5. Edit terraform.tfvars file with your tenancy information
6. Execute terraform apply command and wait until process completed.
7. RedHat OpenShift Console will show amber color warning when Instances got boot back to the live ISO (Expected Situation). 
8.Please note that the OpenShift Console will take upto 5-10 mins to show up instance upon creation. So have some patience on the process.
9. Now, goto the openshift console, you can see the assisted cluster is ready.
if you find "disk insufficient error, make sure that, NVME diask has been selected for booting.

![image](https://user-images.githubusercontent.com/26675416/146725950-dd02d4ed-bccc-4a59-bb5a-ef35b914b4e9.png)

9. click on next for the cluster installation.
10. once the installation is complete, you can use the credentials to login to the cluster nodes.

![image](https://user-images.githubusercontent.com/26675416/146726221-67f97301-0676-44a6-9b25-770f86451b23.png)

Please make sure to download kubeconfig file from OpenShift Assisted Cluster Installation page and it will be available to download from the console for 20 days..

### Note on Deployment Security
Please note that this is a Proof of Concept for running OpenShift on Oracle Cloud Infrastructure. Please review security using provided tools on Oracle Cloud to ensure that your installation is fully secured against known threats before going to production

### Must do Actions
Please make sure to Terminate or Power Off the instance used to create iPXE environment. Instance Name -> iPXE Web Server.

### Ports Exposed to Public Internet
Port 80 and 443 being exposed to public internet on this setup. Kubernates API not exposed to internet by default and please add new Listener / Backend Set and Backend towards Private LB's IP and Port 6443 then you will have to change api dns record to have Public IP of the Public Loadbalancer

