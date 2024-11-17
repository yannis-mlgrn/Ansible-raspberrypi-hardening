# Ansible-raspberrypi-hardening
A ansible recipe to secure your raspberry pi

## Prerequisites

Before running the Ansible playbook, ensure you provide your private SSH key to enable secure connection to your Raspberry Pi. Follow these steps to configure everything correctly:

### 1. **Ensure You Have a Private SSH Key**

Make sure you have a private SSH key on your machine. By default, it is located at `~/.ssh/id_rsa`. If you don’t have one, generate it with:

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

### 2. **Copy Your Public Key to the Raspberry Pi**

To allow Ansible to connect via SSH, you need to copy your public key to the Raspberry Pi:

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub pi@<raspberry_pi_ip>
```

Replace `<raspberry_pi_ip>` with the IP address of your Raspberry Pi.

### 3. **Update the Inventory File**

In the `inventory.yml` file, configure Ansible to use your private key for connecting:

```yaml
raspberrypi:
  hosts:
    <raspberry_pi_ip>:
      ansible_user: pi
      ansible_ssh_private_key_file: ~/.ssh/id_rsa
```

Replace `<raspberry_pi_ip>` with the IP address of your Raspberry Pi.

### 4. **Test the Connection**

Before running the playbook, verify the SSH connection with Ansible:

```bash
ansible -i inventory.yml raspberrypi -m ping
```

If the setup is correct, you should see a `pong` response.

## Running the Playbook

Once everything is configured, you can run the hardening playbook:

```bash
ansible-playbook -i inventory.yml raspberrypiHardening.yml
```

This command will apply the security configurations to your Raspberry Pi.