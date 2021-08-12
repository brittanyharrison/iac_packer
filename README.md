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

Verify your installation by using the command `packer`

#### Build an AMI 

