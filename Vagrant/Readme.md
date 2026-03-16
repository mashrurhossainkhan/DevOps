# Vagrant Practice – Infrastructure Automation

This repository contains my learning notes and practice commands while learning **Vagrant** for DevOps and Infrastructure as Code (IaC).

Vagrant helps developers create and manage **reproducible development environments** using virtual machines.

---

# What I Learned

- What Vagrant is and why it is used in DevOps
- How to create virtual machines using Vagrant
- Working with **Vagrantfile**
- Managing multiple VMs
- Provisioning servers automatically
- Using **private networks and static IPs**
- Connecting to VMs using SSH
- Destroying and recreating infrastructure easily

---

# Tools Used

- Vagrant
- VirtualBox
- Ubuntu Linux
- MacOS terminal

---

# Basic Vagrant Workflow

### 1. Initialize a Vagrant project

```bash
vagrant init ubuntu/bionic64
```

This creates a **Vagrantfile**.

---

### 2. Start the virtual machine

```bash
vagrant up
```

Vagrant downloads the base box and starts the VM.

---

### 3. SSH into the VM

```bash
vagrant ssh
```

---

### 4. Stop the VM

```bash
vagrant halt
```

---

### 5. Restart the VM

```bash
vagrant reload
```

---

### 6. Destroy the VM

```bash
vagrant destroy
```

This removes the VM completely.

---

# Example Multi-VM Setup

Example `Vagrantfile` with multiple machines:

```ruby
Vagrant.configure("2") do |config|

  config.vm.define "web01" do |web|
    web.vm.box = "ubuntu/bionic64"
    web.vm.network "private_network", ip: "192.168.56.11"
  end

  config.vm.define "web02" do |web|
    web.vm.box = "ubuntu/bionic64"
    web.vm.network "private_network", ip: "192.168.56.12"
  end

  config.vm.define "db01" do |db|
    db.vm.box = "ubuntu/bionic64"
    db.vm.network "private_network", ip: "192.168.56.13"
  end

end
```

Start all VMs:

```bash
vagrant up
```

SSH into a specific machine:

```bash
vagrant ssh web01
```

---

# Networking Concepts Learned

### Private Network

Used for communication between VMs.

Example:

```ruby
config.vm.network "private_network", ip: "192.168.56.10"
```

---

### Public Network (Bridge)

Allows the VM to appear on the same network as the host.

```ruby
config.vm.network "public_network"
```

---

# Useful Vagrant Commands

Check VM status

```bash
vagrant status
```

Reload configuration

```bash
vagrant reload
```

Check logs

```bash
vagrant ssh
```

Destroy infrastructure

```bash
vagrant destroy
```

---

# Why Vagrant is Useful in DevOps

- Creates **consistent environments**
- Easy infrastructure recreation
- Supports **Infrastructure as Code**
- Helps test distributed systems
- Useful for **Ansible, Docker, Kubernetes labs**

---

# Future Plan

Next steps in my DevOps learning:

- Provision servers with **Ansible**
- Automate VM setup
- Integrate with **Docker**
- Simulate production environments

---

# Author

Mashrur Hossain Khan
