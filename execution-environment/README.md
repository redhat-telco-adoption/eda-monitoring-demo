# EDA Monitoring Demo Execution Environment

This repository contains the configuration files for an Ansible Execution Environment (EE) designed for the EDA Monitoring Demo. The EE is tailored for AWS automation tasks and is compatible with Ansible Automation Platform 2.4 and later.

## Contents

- `execution-environment.yml`: Main configuration file for the EE
- `files/requirements.yml`: Ansible collections to be installed
- `files/requirements.txt`: Python package dependencies
- `files/bindep.txt`: System-level dependencies

## Features

- Based on Red Hat Enterprise Linux 9 (RHEL9) minimal image
- Configured for AWS operations with necessary Python packages and Ansible collections
- Set up to use multiple Galaxy servers (published, validated, community)
- Includes diagnostic steps in the build process

## Prerequisites

- Ansible Builder (`ansible-builder`)
- Podman or Docker
- Access to Red Hat registries (for base image)
- Automation Hub token for accessing Red Hat validated content

## Building the Execution Environment

1. Ensure you have the prerequisites installed and configured.

2. Build the execution environment, passing the Automation Hub token as a build argument:
   ```
   ansible-builder build -t eda-monitoring-demo-ee:latest --build-arg CONTENT_HUB_TOKEN=your_token_here
   ```

   Replace `your_token_here` with your actual Automation Hub token.

## Usage

After building, you can use this execution environment with Ansible Navigator or push it to a container registry for use with Ansible Automation Platform.

Example usage with Ansible Navigator:

```
ansible-navigator run your_playbook.yml -e eda-monitoring-demo-ee:latest
```

## Customization

- Modify `files/requirements.yml` to add or remove Ansible collections
- Update `files/requirements.txt` for Python package dependencies
- Adjust `files/bindep.txt` for system-level packages

## Security Notes

- The `CONTENT_HUB_TOKEN` is passed as a build argument. While this is more secure than embedding it in files, ensure your build process handles this token securely.
- The token is used only during build time and is not stored in the final image.
- Regularly update the base image SHA in `execution-environment.yml` to get the latest security updates.

## Contributing

Contributions to improve the execution environment are welcome. Please submit pull requests or open issues for any enhancements, bug fixes, or suggestions.

## License

[Specify your license here]