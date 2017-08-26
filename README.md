# Genomics Big Compute Lab
WORK IN PROGRESS

## Solution Overview

## IaaS: Linux Virtual Machine (VM) + Genomics software
### 1. Deploy Linux VM
You can use Azure CLI commands to deploy a Linux VM: 

    az network vnet create --resource-group linuxvms --name myVnet --address-prefix 192.168.0.0/16 --subnet-name mySubnet --subnet-prefix 192.168.1.0/24
    az network public-ip create --resource-group linuxvms --name muPublicIP --dns-name kplinuxvmtest
    az network nsg create --resource-group linuxvms --name myNSG
    az network nsg rule create --resource-group linuxvms --nsg-name myNSG --name myNSGruleSSH --protocol tcp --priority 1000 --destination-port-range 22 --access allow
    az network nic create --resource-group linuxvms --name myNIC --vnet-name myVnet --subnet mySubnet --public-ip-address muPublicIP --network-security-group myNSG
    az vm availability-set create --resource-group linuxvms --name myAvailabilitySet
    az vm create --resource-group linuxvms --name myVM --location westeurope --availability-set myAvailabilitySet --nics myNIC --image CentOS --admin-username msadmin --generate-ssh-keys

From the resulting output, find the public IP address.  Then use "ssh msadmin@<public IP address>" to connect to the Linux VM. 

### 2. Deploy Genomics Software
In the accompanying Linux script, __"setup-genomics-software.sh"__, genomics software is downloaded, compiled, and installed to the Linux VM, ready for execution from a folder called /opt/genomics.  You can follow these steps:
* First, download the script to your Linux VM
* Save the script to the root user's home folder (/root)
* Make the script executable (chmod +x setup-genomics-software.sh)
* Execute the script (./setup-genomics-software.sh)

### 3. Test Genomics Workflow


## Microsoft Genomics Service (Preview)

## Using Azure Batch

## More Information
* Broad Institute GATK Best Practices - https://software.broadinstitute.org/gatk/best-practices/
* BLAST demo with Azure - https://github.com/Azure/azure-hpc/tree/master/LifeSciences/AzureBlast
* Microsoft Genomics PaaS Service - https://www.microsoft.com/en-us/research/project/genomicsacceleration/
* Microsoft Genomics Documentation - https://msgen.readthedocs.io/en/latest/ 
* Genomics on Infopedia (MSFT only) - https://microsoft.sharepoint.com/sites/infopedia/search/pages/results.aspx?term=genomics&scope=All
* GATK tutorial at UCLA - https://qcb.ucla.edu/wp-content/uploads/sites/14/2016/03/IntroductiontoVariantCallsetEvaluationandFilteringTutorialAppendix-LA2016.pdf 

## Reporting Bugs & Contributing
For any problems/comments/suggestions, please share with Karl Podesta <kapodest@microsoft.com>
If you wish to fix any problems yourself, please do so and submit a pull request! Thanks!
