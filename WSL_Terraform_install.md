# How to Install WSL ( Windows Sub System Linux - Ubuntu)  

1. Open your CMD prompt on Windows and Run

As part of Installation it will prompt you to set username and password (ex: ubuntu/password)

```
wsl --install
```

2. After the Installation Connect to Ubuntu Machine with the below command

```
wsl -d ubunutu
```

# Terraform Installation Instruction on WSL Based Ubuntu Machine  

## Install Terraform using HashiCorp's APT Repository  

1. Open your WSL Ubuntu terminal and run  

```
sudo apt update && sudo apt install -y gnupg software-properties-common curl
```

2. Add the HashiCorp GPG key  

```
wget -O - https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
```


3. Add the HashiCorp repository to your APT sources

```
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
```

4. Update your package list again to include the new repository

```
sudo apt update
```


5. Install Terraform

```
sudo apt install terraform
```


6. Verify Terraform

```
terraform --version
```

   
