# AzureAnsiblePlaybooks
Using Ansible Playbooks to deploy infrastructure in Azure

# Overview
Ansible is a configuration manager to help create, update and maintain cloud resources 

# Installation
To install Ansible Azure On Mac OSX:

``` pip install ansible[azure] ```

For development on VS Code highly recommend installing the Ansible extension

## Setting up Azure Credentials for the playbooks

In order to run the playbooks and deploy resources in Azure, you need to set the right credentials for the subscription you intend to use. There are multiple ways to set it up.

- Azure login:

        az login
        (or)
        az login --tenant <tenant id>
        (or)
        az account set --subscription <subscription id>

- Azure Cloud Shell login:

         You can right click on the playbook to execute and choose Run in Azure Cloud Shell. This will walk you through logging in interactively.

- Azure Credentials file: 

        Add the following variables into /home/username/.azure/credentials 

        [default]
        subscription_id=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
        client_id=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
        secret=xxxxxxxxxxxxxxxxx
        tenant=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
        
- Set up environment variables

        AZURE_CLIENT_ID
        AZURE_SECRET
        AZURE_SUBSCRIPTION_ID
        AZURE_TENANT

# How to Run

1. To simply execute a playbook,

    ``` ansible-playbook /path/to/playbook.yml ```

2. If you need to store your variables in a separate file and would like to include it during execution, 

    ``` ansible-playbook /path/to/playbook.yml --extra-vars /path/to/variables.yml ```

3. If executing the playbook in Azure Cloud Shell, then you need to make sure the variables file is stored in the storage account linked to your cloud shell

# Ansible Tower

Ansible Tower is .. <TBD>

# Resources
- Ansible Documentation: https://docs.ansible.com/
- Ansible Azure Guide: https://docs.ansible.com/ansible/2.5/scenario_guides/guide_azure.html
- 

# Notes
- By default, the desired end state for the resources is "present" implying that when playbooks are executed they are either created or updated unless otherwise explicitly mentioned. If 'absent', then the playbook ends up deleting the resources in the cloud
- When writing an Ansible playbook, it's the responsibility of the developer to ensure idempotency and hierarchy. 
- Ansible doesn't ensure dependency between resources. For example, if you are creating a VM, then all necessary resources for it say IP, NIC, etc.. needs to be created before in the playbook. Order matters
- 