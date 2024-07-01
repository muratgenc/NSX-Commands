Step 1: Store Credentials in Terraform Enterprise
Create a Terraform Enterprise Workspace:
Navigate to your Terraform Enterprise dashboard and create a new workspace.
Add environment variables in the workspace settings:
```
ANSIBLE_USER (value: your_service_account)
ANSIBLE_PASSWORD (value: your_service_account_password)
```
Step 2: Create Terraform Configuration to Retrieve Credentials
Create a file named vault.tf to configure Terraform to retrieve the credentials from TFE:

```
provider "tfe" {
  hostname = "your_tfe_hostname" # e.g., app.terraform.io for Terraform Cloud, or your self-hosted instance
  token    = "your_tfe_api_token"
}

data "tfe_variable" "ansible_user" {
  organization = "your_tfe_organization"
  workspace    = "your_tfe_workspace"
  name         = "ANSIBLE_USER"
}

data "tfe_variable" "ansible_password" {
  organization = "your_tfe_organization"
  workspace    = "your_tfe_workspace"
  name         = "ANSIBLE_PASSWORD"
}

output "ansible_user" {
  value     = data.tfe_variable.ansible_user.value
  sensitive = true
}

output "ansible_password" {
  value     = data.tfe_variable.ansible_password.value
  sensitive = true
}
```

Step 3:Run the following commands to initialize Terraform, apply the configuration, and retrieve the credentials:
```
terraform init
terraform apply
```
Step 4: Set Environment Variables
```
export ANSIBLE_USER=your_retrieved_user
export ANSIBLE_PASSWORD=your_retrieved_password
```

Step 5: Create Ansible Inventory File
```
[esxi_hosts]
esxi_host ansible_host=your_esxi_host_ip ansible_user={{ lookup('env', 'ANSIBLE_USER') }} ansible_ssh_common_args='-o StrictHostKeyChecking=no'
```
Step 6: Create Ansible Playbook
Create or update the Ansible playbook run_nscli_with_prompt.yml:

Step 7: Run the Playbook
```ansible-playbook -i hosts.ini run_nscli_with_prompt.yml```
