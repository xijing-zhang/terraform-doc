# Getting Started with Terraform

Terraform is the most popular declarative coding tool for defining and provisioning infrastructure as code (IaC). In this short tutorial for a Linux platform, you will install Terraform and create a configuration file representing the desired state of your infrastructure. 

## Prerequisites

To complete this tutorial, you will need:

 - A Command Line Interface (CLI) client on your Linux machine

## Install Terraform

Visit [Terraform.io](https://www.terraform.io/downloads.html) to download the proper binary package for your operating system and architecture.

Unzip the package in your `Downloads` and move it to the `/usr/local/bin/` folder.

  ```shell
  $ mv ~/Downloads/terraform /usr/local/bin/
  ```

## Create a Terraform Configuration

We recommend creating a new directory on your local machine to store your Terraform configuration code.

  ```shell
  $ mkdir terraform-demo
  $ cd terraform-demo
   ```

Next, create a file for your Terraform configuration code.

  ```shell
  $ touch main.tf
  ```

Paste the following lines into the file.

  ```hcl
  provider "docker" {
      host = "unix:///var/run/docker.sock"
  }

  resource "docker_container" "nginx" {
    image = docker_image.nginx.latest
    name  = "training"
    ports {
      internal = 80
      external = 80
    }
  }

  resource "docker_image" "nginx" {
    name = "nginx:latest"
  }
  ```

Next, install the Docker provider by initializing Terraform with the `init` command. 

  ```shell
  $ terraform init
  ```

Check for any errors. Once initialized successfully, provision the resource with the `apply` command. When Terraform prompts you to confirm, type `yes` and hit `ENTER`.

  ```shell
  $ terraform apply
  ```

The command takes a few minutes to run and displays a message indicating that the resource was created.

Finally, `destroy` the infrastructure. When Terraform prompts you to confirm, type `yes` and hit `ENTER`.

  ```shell
  $ terraform destroy
  ```

You've now used Terraform to successfully provision and destroy a Docker resource.

## Next Steps

In this tutorial, you installed Terraform on your Linux system and used it to successfully provision and destroy a Docker resource. Now that your Terraform configuration code is set up, you can reproduce and tear down the same production environment with one CLI command each. You can modify this configuration code to support other services and create different resources. Terraform is a powerful, cloud-agnostic IAC provisioning tool that helps you modify, rebuild, and track changes to the infrastructure.

If you'd like to learn more on how to get started with Terraform, please visit the [Introduction to Terraform](https://www.terraform.io/intro/index.html) page. To learn more about using Terraform with the Docker provider, please visit the [Docker Provider](https://www.terraform.io/docs/providers/docker/index.html) page.

