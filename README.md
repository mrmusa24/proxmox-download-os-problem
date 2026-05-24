# proxmox-download-os-problem
একটা command run করো — এটা reinstall + symlink fix + service restart করবে:

apt install --reinstall wget -y && ln -sf /usr/bin/wget /bin/wget && systemctl restart pvedaemon pveproxy pvestatd

তারপর verify:

which wget
ls -l /usr/bin/wget
ls -l /bin/wget

Expected:

/usr/bin/wget

তারপর template update/download:

pveam update
pveam download local ubuntu-24.04-standard_24.04-2_amd64.tar.zst

যদি still same issue আসে, এই exact command run করে output দাও:

/usr/bin/wget --version
echo $PATH

Most likely /bin/wget symlink missing — উপরের first command দিলেই fix হবে।

akta .md file kore den 

Boss, এইটা .md file content হিসেবে save করো (যেমন: proxmox-fix.md)
তারপর step by step run করো।

# Proxmox Template Download Fix

## Problem
TASK ERROR: download failed: open3: exec of wget failed

---

## Step 1: Reinstall wget

```bash
apt install --reinstall wget -y
Step 2: Fix wget symlink
ln -sf /usr/bin/wget /bin/wget
Step 3: Restart Proxmox services
systemctl restart pvedaemon
systemctl restart pveproxy
systemctl restart pvestatd
Step 4: Verify wget
which wget
ls -l /usr/bin/wget
ls -l /bin/wget

Expected output:

/usr/bin/wget
Step 5: Update template list
pveam update
Step 6: Download Ubuntu template
pveam download local ubuntu-24.04-standard_24.04-2_amd64.tar.zst
One-line Fix
apt install --reinstall wget -y && ln -sf /usr/bin/wget /bin/wget && systemctl restart pvedaemon pveproxy pvestatd
If Still Not Working

Check:

/usr/bin/wget --version
echo $PATH

Server এ file create করতে চাইলে:

```bash
cat > proxmox-fix.md

তারপর উপরের content paste করে
Ctrl + D চাপো।
