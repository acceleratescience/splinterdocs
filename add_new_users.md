# Adding a new user to Splinter
# (Admin Only)

## General notes

* Username is the lead CRSid, lowercase.
* One team can share one username with multiple SSH keys.
* Do not give sudo access unless needed.
* Feel free to skip the verify steps

## Instructions

### 1. Create user

```bash
sudo adduser --disabled-password --gecos "" newusername
```

Verify:

```bash
getent passwd newusername
```

### 2. Set up SSH keys
- One key is fine too
- Can add a key of yours to test things

```bash
sudo mkdir -p /home/newusername/.ssh

sudo tee /home/newusername/.ssh/authorized_keys > /dev/null <<'EOF'
ssh-ed25519 key1 comment1
ssh-ed25519 key2 comment2
ssh-ed25519 key3 comment3
EOF

sudo chown -R newusername:newusername /home/newusername/.ssh
sudo chmod 700 /home/newusername/.ssh
sudo chmod 600 /home/newusername/.ssh/authorized_keys
```

Verify:

```bash
sudo nl -ba /home/newusername/.ssh/authorized_keys
sudo namei -l /home/newusername/.ssh/authorized_keys
```

### 3. Add user to the allowed list

```bash
sudo nano /etc/ssh/sshd_config.d/10-allowusers.conf
```

Append the username to the existing `AllowUsers` line.

Verify:

```bash
sudo sshd -T | grep -i '^allowusers'
```

### 4. Reload SSH

```bash
sudo sshd -t && sudo systemctl reload ssh
```

Verify:

```bash
sudo systemctl is-active ssh
```

### 5. Test login 
- to be done by user, from machine with their ssh key
- or you if you added your ssh key too

```bash
ssh newusername@splinter.cl.cam.ac.uk
```

Verify errors on the server:

```bash
sudo journalctl -u ssh -f
```
