# Infrastructure as Code(IaC)

Before the advent of IaC, infrastructure management was typically a manual and time-consuming process. System administrators and operations teams had to:

Manually Configure Servers: Servers and other infrastructure components were often set up and configured manually, which could lead to inconsistencies and errors.

**Lack of Version Control:** Infrastructure configurations were not typically version-controlled, making it difficult to track changes or revert to previous states.

**Documentation Heavy:** Organizations relied heavily on documentation to record the steps and configurations required for different infrastructure setups. This documentation could become outdated quickly.

**Limited Automation:** Automation was limited to basic scripting, often lacking the robustness and flexibility offered by modern IaC tools.

**Slow Provisioning:** Provisioning new resources or environments was a time-consuming process that involved multiple manual steps, leading to delays in project delivery.

**Why Terraform?**
There are multiple reasons why Terraform is used over the other IaC tools but below are the main reasons.

**Multi-Cloud Support:** Terraform is known for its multi-cloud support. It allows you to define infrastructure in a cloud-agnostic way, meaning you can use the same configuration code to provision resources on various cloud providers (AWS, Azure, Google Cloud, etc.) and even on-premises infrastructure.

**Large Ecosystem:** Terraform has a vast ecosystem of providers and modules contributed by both HashiCorp (the company behind Terraform) and the community. This means you can find pre-built modules and configurations for a wide range of services and infrastructure components, saving you time and effort in writing custom configurations.

**Declarative Syntax:** Terraform uses a declarative syntax, allowing you to specify the desired end-state of your infrastructure. This makes it easier to understand and maintain your code compared to imperative scripting languages.

**State Management:** Terraform maintains a state file that tracks the current state of your infrastructure. This state file helps Terraform understand the differences between the desired and actual states of your infrastructure, enabling it to make informed decisions when you apply changes.

**Plan and Apply:** Terraform's "plan" and "apply" workflow allows you to preview changes before applying them. This helps prevent unexpected modifications to your infrastructure and provides an opportunity to review and approve changes before they are implemented.

**Integration with Other Tools:** Terraform can be integrated with other DevOps and automation tools, such as Docker, Kubernetes, Ansible, and Jenkins, allowing you to create comprehensive automation pipelines.

**HCL Language:** Terraform uses HashiCorp Configuration Language (HCL), which is designed specifically for defining infrastructure. It's human-readable and expressive, making it easier for both developers and operators to work with.


# Providers

A provider in Terraform is a plugin that enables interaction with an API. This includes cloud providers, SaaS providers, and other APIs. The providers are specified in the Terraform configuration code. They tell Terraform which services it needs to interact with.

For example, if you want to use Terraform to create a virtual machine on AWS, you would need to use the aws provider. The aws provider provides a set of resources that Terraform can use to create, manage, and destroy virtual machines on AWS.

Here is an example of how to use the aws provider in a Terraform configuration:

provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "example" {
  ami = "ami-0123456789abcdef0" # Change the AMI 
  instance_type = "t2.micro"
}

# Different ways to configure providers in terraform
There are three main ways to configure providers in Terraform:

**In the root module**

provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "example" {
  ami = "ami-0123456789abcdef0"
  instance_type = "t2.micro"
}

**In a child module**

module "aws_vpc" {
  source = "./aws_vpc"
  providers = {
    aws = aws.us-west-2
  }
}

resource "aws_instance" "example" {
  ami = "ami-0123456789abcdef0"
  instance_type = "t2.micro"
  depends_on = [module.aws_vpc]
}

**In the required_providers block**

terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
      version = "~> 3.79"
    }
  }
}

resource "aws_instance" "example" {
  ami = "ami-0123456789abcdef0"
  instance_type = "t2.micro"
}

**Multiple Providers**
You can use multiple providers in one single terraform project. For example,

Create a providers.tf file in the root directory of your Terraform project.
In the providers.tf file, define the AWS and Azure providers. For example:

provider "aws" {
  region = "us-east-1"
}

provider "azurerm" {
  subscription_id = "your-azure-subscription-id"
  client_id = "your-azure-client-id"
  client_secret = "your-azure-client-secret"
  tenant_id = "your-azure-tenant-id"
}

**Multiple Region Implementation in Terraform**
You can make use of alias keyword to implement multi region infrastructure setup in terraform.

provider "aws" {
  alias = "us-east-1"
  region = "us-east-1"
}

provider "aws" {
  alias = "us-west-2"
  region = "us-west-2"
}
provider "aws" {
  region = "us-east-1"
}

provider "azurerm" {
  subscription_id = "your-azure-subscription-id"
  client_id = "your-azure-client-id"
  client_secret = "your-azure-client-secret"
  tenant_id = "your-azure-tenant-id"
}

**Provider Configuration**

The required_providers block in Terraform is used to declare and specify the required provider configurations for your Terraform module or configuration. It allows you to specify the provider name, source, and version constraints.

terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 3.0"
    }
    azurerm = {
      source  = "hashicorp/azurerm"
      version = ">= 2.0, < 3.0"
    }
  }
}

# Variables 

Input and output variables in Terraform are essential for parameterizing and sharing values within your Terraform configurations and modules. They allow you to make your configurations more dynamic, reusable, and flexible.

**Input Variables**

Input variables are used to parameterize your Terraform configurations. They allow you to pass values into your modules or configurations from the outside. Input variables can be defined within a module or at the root level of your configuration. Here's how you define an input variable:

variable "example_var" {
  description = "An example input variable"
  type        = string
  default     = "default_value"
}

**Output Variables**

Output variables allow you to expose values from your module or configuration, making them available for use in other parts of your Terraform setup. Here's how you define an output variable:

output "example_output" {
  description = "An example output variable"
  value       = resource.example_resource.example.id
}

Conditional Expressions
Conditional expressions in Terraform are used to define conditional logic within your configurations. They allow you to make decisions or set values based on conditions. Conditional expressions are typically used to control whether resources are created or configured based on the evaluation of a condition.

The syntax for a conditional expression in Terraform is:

condition ? true_val : false_val

# Conditional Expressions

Conditional expressions in Terraform are used to define conditional logic within your configurations. They allow you to make decisions or set values based on conditions. Conditional expressions are typically used to control whether resources are created or configured based on the evaluation of a condition.

The syntax for a conditional expression in Terraform is:

condition ? true_val : false_val

# Built-in Functions

Terraform is an infrastructure as code (IaC) tool that allows you to define and provision infrastructure resources in a declarative manner. Terraform provides a wide range of built-in functions that you can use within your configuration files (usually written in HashiCorp Configuration Language, or HCL) to manipulate and transform data.

1. concat(list1, list2, ...): Combines multiple lists into a single list.
2. element(list, index): Returns the element at the specified index in a list.
3. length(list): Returns the number of elements in a list.
4. map(key, value): Creates a map from a list of keys and a list of values.
5. lookup(map, key): Retrieves the value associated with a specific key in a map.
6. join(separator, list): Joins the elements of a list into a single string using the specified separator.
