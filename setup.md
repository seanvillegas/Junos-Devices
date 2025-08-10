## ✅ Step 1: Ensure the device has SSH installed

Run this on the **serial terminal** (you're already connected):

```bash
which sshd
```

If it returns something like `/usr/sbin/sshd`, then SSH server is installed.

If **not installed**, and the device is Linux-based (like Raspberry Pi):

```bash
sudo apt update
sudo apt install openssh-server
```

---

## ✅ Step 2: Enable and start the SSH service

```bash
sudo systemctl enable ssh
sudo systemctl start ssh
```

Check its status:

```bash
sudo systemctl status ssh
```

You should see something like:

```
● ssh.service - OpenBSD Secure Shell server
   Active: active (running)
```

---

## ✅ Step 3: Find the device’s IP address

Run:

```bash
ip a
```

Or:

```bash
hostname -I
```

Look for something like `192.168.x.x` — that's the IP address on your local network.

---

## ✅ Step 4: Test SSH access from your Mac

On your Mac’s Terminal, run:

```bash
ssh username@192.168.x.x
```

Replace:

* `username` with the login name (e.g. `pi`, `root`, etc.)
* `192.168.x.x` with the device's IP address

---

## ✅ Optional Step 5: Allow SSH root login (not recommended unless necessary)

If you want to allow root login via SSH (disabled by default), edit:

```bash
sudo nano /etc/ssh/sshd_config
```

Find and modify or add:

```bash
PermitRootLogin yes
```

Then restart SSH:

```bash
sudo systemctl restart ssh
```

---

## 🚨 Important Tips

* Make sure the device and your Mac are on the **same network**.
* If there’s a firewall, make sure port **22** is open.
* If you're planning to SSH often, consider setting up **SSH key authentication** instead of using a password.

---

Password for ssh

- xyz987


## MacOS 

1. check firewall
sudo pfctl -d

2. see connection 
sudo tcpdump -i en8 icmp
3. ping 192.168.1.2
4. set mac address to switch and reset the ping so its not in memory
sudo arp -s 192.168.1.2 d8:b1:22:88:ad:ab
5. networksetup -listallhardwareports
6. ifconfig en8 
