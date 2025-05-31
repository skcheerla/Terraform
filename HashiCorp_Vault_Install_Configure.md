# HashiCorp vault Installation and Setup

1. Download Vault

Visit the official HashiCorp Vault download page (https://developer.hashicorp.com/vault/install) and select the appropriate binary or package for your operating system.

2. Vault Install Instructions for Ubuntu Linux 

```
wget -O - https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install vault
```

3. Verify Installed Version

   ```
   vault --version
   ```

4. After Installation: Initial Setup and Configuration (Crucial Steps!)  

Once Vault is installed, you'll need to configure and initialize it. This typically involves:

Creating a configuration file (e.g., vault.hcl): This file defines how Vault listens for requests, where it stores data (storage backend), and other settings. For a basic development setup, you might use:

```
listener "tcp" {
  address = "127.0.0.1:8200"
  tls_disable = true # For dev only, enable TLS for production!
}

storage "file" {
  path = "/opt/vault/data" # Create this directory
}

disable_mlock = true # For dev only, enable mlock for production for security
```

Creating a data directory: The storage "file" backend requires a directory to store Vault's data.

Starting the Vault server:

```
vault server -config=vault.hcl
```
(For development, you can use vault server -dev for a quick, insecure, in-memory instance.)

Initializing Vault: This is a one-time process that generates the master key and initial root token. You'll need to provide a certain number of "key shares" and a "key threshold."  

```
vault operator init
```
IMPORTANT: Securely save the unseal keys and the root token! These are critical for managing your Vault instance.
Unsealing Vault: After initialization, Vault is "sealed" for security. You need to provide a quorum of unseal keys to unseal it and make it operational.

```
vault operator unseal <unseal_key_1>
vault operator unseal <unseal_key_2>
# ... and so on until the threshold is met
```

Logging in: Use the root token obtained during initialization to log in to the Vault CLI or UI:

```
vault login <root_token>
```
Or access the UI at http://127.0.0.1:8200/ui (if tls_disable is true







