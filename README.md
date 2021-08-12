# Packer 

Packer is another Infrastructure as Code tool, which we can use to create an image of a environment. It is very useful when scaling up our infrastructure, as it is far quicker to create environments with a saved image, instead of provisioning each new environment.

## Packer template

A Packer template is a configuration file that defines the image you want to build and how to build it. Packer templates use the Hashicorp Configuration Language (HCL).

## Packer setup 

#### Install Packer 

You can install manually or using Homebrew on OS:
- manual:

    - To install the precompiled binary, [download](https://www.packer.io/downloads) the appropriate package for your system. Packer is currently packaged as a zip file.


- Homebrew:
    - First, install the HashiCorp tap, a repository of all our Homebrew packages.

    ```
    brew tap hashicorp/tap
    ```

    - Now, install Packer with hashicorp/tap/packer.

    ```
    brew install hashicorp/tap/packer
    ```

    - To update to the latest, run

    ```
    brew upgrade hashicorp/tap/packer
    ```
- Linux (Ubuntu):
    - Add the HashiCorp GPG key.
    ```
    curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
    ```

    - Add the official HashiCorp Linux repository.
    ```
    sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
    ```

    - Update and install
    ```
    sudo apt-get update && sudo apt-get install packer
    ```
    
Verify your installation by using the command `packer`

#### Build an AMI 
Packer files are written in JSON

```
{
{
    "variables": {
      "aws_access_key": "{{env `AWS_ACCESS_KEY_ID`}}",
      "aws_secret_key": "{{env `AWS_SECRET_ACCESS_KEY`}}"
    },
    "builders": [
      {
        "type": "amazon-ebs",
        "access_key": "{{user `aws_access_key`}}",
        "secret_key": "{{user `aws_secret_key`}}",
        "region": "eu-west-1",
        "source_ami_filter": {
          "filters": {
            "virtualization-type": "hvm",
            "name": "ubuntu/images/*ubuntu-xenial-16.04-amd64-server-*",
            "root-device-type": "ebs"
          },
          "owners": ["099720109477"],
          "most_recent": true
        },
        "instance_type": "t2.micro",
        "ssh_username": "ubuntu",
        "ami_name": "eng89_brittany_packer_ami"
      }
    ],
    "provisioners": [
      {
        "type": "ansible",
        "playbook_file": "../playbooks/app_playbook.yaml"
      }
    ]
  }
  
```