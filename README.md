# MERN_Terraform_Ansible_IaaS
We are deploying a MERN application using Terraform and Ansible on Ubuntu

### Part 1: Infrastructure Setup with Terraform

  AWS Setup and Terraform Initialization:

On Ubuntu from
```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
sudo apt install unzip
unzip awscliv2.zip
sudo ./aws/install
```
test it using "aws --version" if response is like below then aws is properly configured.

![image](https://github.com/Sthatikonda8161/MERN_Terraform_Ansible_IaaS/assets/136583514/51ba2891-aec2-4ed7-ad0f-10b542134502)


Configure aws using the "aws configure" command before that We have to download the AWS Console access key.

For that, go to My Security Credentials ( Top right ) > choose Access keys > Create New Access Key, then download that key to the local machine.

![image](https://github.com/Sthatikonda8161/MERN_Terraform_Ansible_IaaS/assets/136583514/3ceb798d-64ac-4e7a-8bf2-83aaa960ef69)

Now configure your account 
```
aws configure
```
Initialize a new Terraform project targeting AWS on Ubuntu

  - Ensure that your system is up to date and you have installed the gnupg, software-properties-common, and curl packages installed. You will use these packages to verify HashiCorp's GPG signature and install HashiCorp's Debian package repository.

```
sudo apt-get update && sudo apt-get install -y gnupg software-properties-common
```

 - Install the HashiCorp GPG key.
```
wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg

```
- Verify the key's fingerprint.
```
gpg --no-default-keyring \
--keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg \
--fingerprint

```
- The gpg command will report the key fingerprint:
![image](https://github.com/Sthatikonda8161/MERN_Terraform_Ansible_IaaS/assets/136583514/79190b9b-9af0-40a0-bc18-c7aaad992a22)

  
- Add the official HashiCorp repository to your system. The lsb_release -cs command finds the distribution release codename for your current system, such as buster, groovy, or sid.
```
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list

```  
- Download the package information from HashiCorp.
```
sudo apt update
```
- Install Terraform from the new repository.
```
  sudo apt-get install terraform
```
 - verify the installation.
   
![image](https://github.com/Sthatikonda8161/MERN_Terraform_Ansible_IaaS/assets/136583514/2a6f3257-64a7-4cc0-92fb-99cf4528cd1b)

 
Create a new directory for the project
```
mkdir terraform-aws
cd terraform-aws
touch main.tf
```
Initialize Terraform
```
terraform init
```


