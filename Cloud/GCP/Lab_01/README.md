# Infrastructure as Code (IaC) with Terraform (Google Cloud)

## 📌 Overview
This lab demonstrates how to use **Terraform** to manage infrastructure on **Google Cloud Platform (GCP)**. You will learn how to configure Terraform, define resources, and perform lifecycle operations such as creation, modification, and deletion.

## 🎯 Objective
By completing this lab, you will:

- Using Google Cloud the following tasks will be performed:
- Verify Terraform installation
- Define Google Cloud as the provider
- Create, change and destroy Google Cloud resources by using Terraform

## 🧰 Prerequisites

- Google Cloud account
- Access to **Google Cloud Shell**
- Basic understanding of cloud infrastructure concepts
- Terraform installed (pre-installed in Cloud Shell)

---

## 🚀 Getting Started

### Step 1 - Check terraform installation

1. On the Google Cloud Menu, Click on **Activate Cloud Shell** and the cloud shell will be opened.  
2. Confirm that Terraform is installed by running the command:
```bash
terraform --version
```

The output will be:   
![Screenshot](./terraform_version.png)

### Step 2 - Add Google Cloud Provider

1. Create the ```main.tf``` file
```bash
touch main.tf
```
2. Click **Open Editor** on the toolbar of Cloud Shell. Click **Open in a new window** to leave the Editor open in a separate tab.
3. Copy the following code in the ```main.tf``` file.
```bash
terraform {
  required_providers {
    google = {
      source = "hashicorp/google"
    }
  }
}

provider "google" {

  project = "Project ID"
  region  = "Region"
  zone    = "Zone"
}
```
4. Click **File > Save**
5. Switch to the Cloud Shell and run the terraform init command.
``` bash
terraform init
```
### Step 2 - Build the Infrastructure
Creat a compute instance without specifying the network parameter.

1. Switch to the editor window. Within the ```main.tf``` file, enter the following code.
```bash
resource "google_compute_instance" "terraform" {
  name         = "terraform"
  machine_type = "e2-micro"
  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-11"
    }
  }
}
```
2. Save the ```main.tf``` file by clicking **File > Save**.
3. Run the following command to preview if the compute engine will be created.
``` bash
terraform plan
```
4. The configuration fails with the following error. This is because you cannot configure a compute engine without a network.

