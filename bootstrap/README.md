# EDA Monitoring Demo Bootstrap Playbook

This playbook sets up the necessary components in Ansible Automation Platform (AAP) for the EDA Monitoring Demo.

## Prerequisites

- Ansible (version 2.9 or later)
- `ansible.controller` collection
- Access to an Ansible Automation Platform instance
- AWS account with appropriate permissions

## Installation

1. Install the required Ansible collection:

   ```
   ansible-galaxy collection install ansible.controller
   ```

2. Clone this repository:

   ```
   git clone https://github.com/redhat-telco-adoption/eda-monitoring-demo.git
   cd eda-monitoring-demo/bootstrap
   ```

3. Create a `vars/bootstrap_vars.yml` file with the following content (adjust values as needed):

   ```yaml
   ---
   project_name: "eda-monitoring-demo"
   aap_organization: "Your Organization"
   aap_hostname: "your-aap-hostname"
   aap_username: "your-aap-username"
   aap_password: "your-aap-password"

   aws_access_key: "your-aws-access-key"
   aws_secret_key: "your-aws-secret-key"
   aws_session_token: "your-aws-session-token"  # Optional, for temporary credentials

   project_repo_url: "https://github.com/redhat-telco-adoption/eda-monitoring-demo.git"

   ee_image: "quay.io/redhat-telco-adoption/eda-monitoring-demo-ee"

   vault_password: "your-vault-password"
   ```

## Usage

Run the bootstrap playbook:

```
ansible-playbook bootstrap.yml
```

This playbook will:

1. Create an AAP organization
2. Create AWS, AAP, and Vault credentials
3. Set up a project linked to your Git repository
4. Create an execution environment using the specified image
5. Set up an inventory
6. Create job templates for AWS provisioning and host management (with Vault credential)
7. Create a workflow template that combines the AWS provisioning and host management jobs

## Customization

You can customize the playbook by modifying the `vars/bootstrap_vars.yml` file. Adjust variables such as `project_name`, `aap_organization`, `ee_image`, `vault_password`, and others to fit your specific requirements.

## Troubleshooting

- Ensure that your AAP credentials are correct and have sufficient permissions.
- The playbook is set to not validate SSL certificates (`validate_certs: false`). If you need to enable certificate validation, you'll need to modify the playbook.
- Make sure your AWS credentials have the necessary permissions for creating resources.
- Verify that the specified execution environment image is accessible from your AAP instance.
- Ensure that the Vault password is correct and matches the one used to encrypt any vault files in your project.

## Contributing

If you'd like to contribute to this project, please submit a pull request or open an issue on the GitHub repository.

