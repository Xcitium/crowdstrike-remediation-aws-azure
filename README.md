
# CrowdStrike BSoD Remediation for Azure and AWS workloads

The aim of this tool is to remove the problematic Crowdstrike updates that causes the BSoD on startup in an automated way. For Azure and AWS environments below recovery options are available. 
https://techcommunity.microsoft.com/t5/azure-compute-blog/recovery-options-for-azure-virtual-machines-vm-affected-by/ba-p/4196798

https://repost.aws/knowledge-center/ec2-instance-crowdstrike-agent

In cases where above solutions does not work or not applicable, you can apply this solution. Our solution first detach the disk from VMs and remove corrupted sys files form file system and finally attach and reboot the VM/

## Description of Azure Remediation

This project provides a Python script to fix Azure Virtual Machine (VM) disks from Crowdstrike issue using the Azure SDK for Python. The script includes functionalities to attach and detach data disks from Azure VMs, leveraging Azure Identity for authentication and the Azure Compute Management Client for VM operations.

### Prerequisites
1. Download and install [az cli](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-linux)
2. Configure `az login` such that it points to the right account/subscription
3. Install jq

### Installation

1. **Clone the repository:**
   \`\`\`bash
   git clone <repository-url>
   cd <repository-directory>
   \`\`\`

2. **Install required packages:**
   \`\`\`bash
   pip install -r requirements.txt
   \`\`\`

### Usage

#### Command Line Example

\`\`\`bash
python3 main.py --csp azure \
        --instances instance_name1,inst2 \
        --resource-group myResourceGroup \ 
        --subscription-id xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
\`\`\`

#### Script Functions

- **detach_vol**: Detach a data disk from a VM.
- **attach_vol**: Attach a data disk to a VM.
- **get_dev_name**: Get the device name of the NTFS disk.
- **check_disk**: Check and handle disk operations (detach, mount, attach).
- **handle_azure**: Main function to handle Azure VM operations.

## Description of AWS Remediation

### Prerequisites
1. Download and install [aws cli](https://aws.amazon.com/cli/)
1. aws credentials are configured using `aws configure`
2. the region in the credentials are set properly

### Installation

1. **Clone the repository:**
   \`\`\`bash
   git clone <repository-url>
   cd <repository-directory>
   \`\`\`

2. **Install required packages:**
   \`\`\`bash
   pip install -r requirements.txt
   \`\`\`

### Usage

#### Command Line Example

\`\`\`bash
python3 main.py --csp aws --instances i-0123456789abcdef0,i-0abcdef1234567890
\`\`\`

#### Script Functions

- **detach_volumes**: Detach all volumes from an EC2 instance.
- **attach_vol**: Attach a volume to an EC2 instance.
- **detach_vol**: Detach a volume from an EC2 instance.
- **start_instance**: Start an EC2 instance.
- **stop_instance**: Stop an EC2 instance.
- **handle_aws**: Main function to handle AWS EC2 operations.

### Logs

The script uses Python's \`logging\` module to log information and errors. Logs can be found in the console output.

## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.

## Disclaimer

This script is provided "as-is" without any warranty. It is not our responsibility for any damages or issues caused by using this script. Always test the script in a non-production environment first and ensure you have a complete backup before proceeding with any operations.

## Acknowledgments

- [AccuKnox](https://accuknox.com)
- [Xcitium](https://xcitium.com)


