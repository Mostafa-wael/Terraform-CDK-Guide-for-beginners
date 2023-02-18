# Terraform CDK Guide for beginners
The Cloud Development Kit for Terraform (CDKTF) enables you to define and provision infrastructure using familiar programming languages. This provides access to the entire Terraform ecosystem without the need to learn HashiCorp Configuration Language (HCL) and allows you to leverage the power of your existing toolchain for testing, dependency management, and so on.

## What are we doing here?
In this article, we will not dive deep into how the CDK work, we would rather start by creating our first project and see it in action!

Terraform currently supports TypeScript, Python, Java, C#, and Go. You can use whatever language you wish. In this article, we will use Python.

## Prerequisites
- Follow the [Getting Started](https://developer.hashicorp.com/terraform/tutorials/cdktf/cdktf-install) guide to install the CDKTF Toolkit.
- Or, install the CDKTF Toolkit using the following commands:
    ``` bash
        sudo apt install python3.10-venv
        pip3 install --user pipx
        pipx install pipenv
        sudo npm install --global cdktf-cli@latest
        cdktf help
    ```

## Basic Commands
1. `cdktf init` - Initialize a new CDKTF project.
2. `cdktf get` - Install all required modules.
3. `cdktf synth` - Synthesize the Terraform configuration.
4. `cdktf deploy` - Deploy the Terraform configuration.
5. `cdktf destroy` - Destroy the Terraform configuration.
6. `cdktf diff` - Show the diff between the current and last deployed configuration.
7. `cdktf watch` - Watch for changes and automatically deploy them.
8. `cdktf output` - Show the outputs of the Terraform configuration.
9. `cdktf console` - Open a console to interact with the Terraform configuration.
10. `cdktf docs` - Open the documentation for the Terraform configuration.

## Our Example
In this example, we will create a Docker container using the Docker provider. We will use the Python programming language. Our goal is to provision an NGINX server using Docker Desktop on Mac, Windows, or Linux. So that, you don’t have to test on any cloud provider and things are much simpler.
This is the HCl code that we will convert to Python using the CDKTF.

``` hcl
    resource "docker_image" "nginx" {
    name         = "nginx:latest"
    keep_locally = false
    }

    resource "docker_container" "nginx" {
        image = docker_image.nginx.name
        name  = "tutorial"
        ports {
            internal = 80
            external = 8000
        }
    }
```
## Procedures
1. Create a new directory for your project.
2. Run `cdktf init --template=python --providers=kreuzwerker/docker --local`.
   1. The `--local` flag prevents CDKTF from using Terraform Cloud.
   2. The `--template=python` flag uses Python as the programming language.
   3. The `--providers=kreuzwerker/docker` flag uses the Docker provider.
3. Add your code in the main file.
4. Compile the code and provision your infrastructure: `cdktf deploy` .
   1. CDKTF will print out a report of the changes that Terraform will make to your infrastructure.
   2. Choose **Approve** to apply these changes.
5. To Destroy the infrastructure: `cdktf destroy`.
   1. Select **Approve** to approve the removal of your container.