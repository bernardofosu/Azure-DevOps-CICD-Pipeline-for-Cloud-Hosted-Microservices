# 🌟 Fix EC2 "No Space Left on Device" + Expand EBS Volume

## 🚀 Step-by-Step Guide

------------------------------------------------------------------------

## 🧩 Why This Happens

Your EBS volume was increased in AWS, but the Linux root partition **did
not auto-expand**, causing:

-   ❌ No space left on device\
-   ❌ Docker build failures\
-   ❌ `apt update` errors\
-   ❌ System instability

------------------------------------------------------------------------

## 🛑 STEP 1 --- Free 1--2GB Immediately

### 🔥 1️⃣ Remove unused Docker data

    sudo docker system prune -a -f

### 🔥 2️⃣ Remove unused Docker volumes

    sudo docker volume prune -f

### 🔥 3️⃣ Clean APT cache

    sudo rm -rf /var/lib/apt/lists/*
    sudo rm -rf /var/cache/apt/*
    sudo apt clean

### 🔥 4️⃣ Clean system logs

    sudo journalctl --vacuum-size=50M

### 🔍 Check free space

    df -h

You need **at least 500MB free** before resizing.

------------------------------------------------------------------------

## 💽 STEP 2 --- Expand EBS Volume in AWS Console

1️⃣ Open **EC2 → Elastic Block Store → Volumes**\
2️⃣ Select your instance volume\
3️⃣ **Actions → Modify Volume**\
4️⃣ Increase size (e.g., 30GB → 100GB)\
5️⃣ Confirm changes

⚡ No reboot required!

------------------------------------------------------------------------

## 🧰 STEP 3 --- Resize Partition on EC2

### 📦 Install growpart

    sudo apt update
    sudo apt install cloud-guest-utils -y

### 📏 Expand the root partition

    sudo growpart /dev/xvda 1

### 🧱 Resize EXT4 filesystem

    sudo resize2fs /dev/xvda1

------------------------------------------------------------------------

## ✅ STEP 4 --- Verify Expansion

    df -h

You should now see:

    /dev/root  30G  ...  

🎉 Success! Disk expanded & system stable.

------------------------------------------------------------------------

## ⚠️ Why Errors Happened

APT & Docker couldn't write files because root was 100% full:

    write error (28: No space left on device)

Freeing space → allows commands\
Resizing → permanently fixes the issue

------------------------------------------------------------------------

✨ Let me know if you want this exported as **PDF**, **DOCX**, or a
**Canva template**!
