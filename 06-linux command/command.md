#  Linux Command Cheat Sheet

এই ফাইলে লিনাক্সের প্রাথমিক (Basic) থেকে শুরু করে প্রয়োজনীয় সব কমান্ড এবং সেগুলোর কাজ সহজ ভাষায় তুলে ধরা হলো।

---

##  ১. ফাইল এবং ডিরেক্টরি সম্পর্কিত কমান্ড (File & Directory Management)

| Command | Definition / কাজ | Example / উদাহরণ |
| :--- | :--- | :--- |
| `pwd` | **Print Working Directory:** আপনি বর্তমানে কোন ফোল্ডারে আছেন তা দেখায়। | `pwd` |
| `ls` | **List:** বর্তমান ডিরেক্টরির ফাইল ও ফোল্ডারের তালিকা দেখায়। | `ls` |
| `ls -la` | হিডেন (লুকানো) ফাইলসহ বিস্তারিত তথ্য দেখায়। | `ls -la` |
| `cd [dir]` | **Change Directory:** এক ফোল্ডার থেকে অন্য ফোল্ডারে প্রবেশ করতে ব্যবহৃত হয়। | `cd Documents` |
| `cd ..` | এক ধাপ আগের (প্যারেন্ট) ডিরেক্টরিতে ফিরে যায়। | `cd ..` |
| `cd ~` | ইউজার হোম (Home) ডিরেক্টরিতে ফিরে যায়। | `cd ~` |
| `mkdir [dir]` | **Make Directory:** নতুন একটি ফোল্ডার তৈরি করে। | `mkdir my_folder` |
| `rmdir [dir]` | ফাঁকা ফোল্ডার মুছে ফেলার জন্য ব্যবহৃত হয়। | `rmdir empty_folder` |
| `rm [file]` | **Remove:** কোনো ফাইল মুছে ফেলে। | `rm file.txt` |
| `rm -rf [dir]` | যেকোনো ফোল্ডার ও তার ভেতরের সবকিছু জোরপূর্বক (forcefully) মুছে ফেলে। | `rm -rf my_folder` |
| `cp [src] [dest]` | **Copy:** ফাইল বা ফোল্ডার কপি করে। | `cp file1.txt file2.txt` |
| `mv [src] [dest]` | **Move/Rename:** ফাইল বা ফোল্ডার এক স্থান থেকে অন্য স্থানে সরায় অথবা রিনেম করে। | `mv old.txt new.txt` |
| `touch [file]` | নতুন ফাঁকা (Empty) ফাইল তৈরি করে। | `touch index.html` |

---

##  ২. ফাইল পড়া ও এডিট করার কমান্ড (File Viewing & Editing)

| Command | Definition / কাজ | Example / উদাহরণ |
| :--- | :--- | :--- |
| `cat [file]` | ফাইলের পুরো কনটেন্ট টার্মিনালে প্রদর্শন করে। | `cat README.md` |
| `head -n [file]` | ফাইলের শুরুর নির্দিষ্ট সংখ্যক লাইন দেখায়। | `head -n 10 file.txt` |
| `tail -n [file]` | ফাইলের শেষের নির্দিষ্ট সংখ্যক লাইন দেখায়। | `tail -n 10 log.txt` |
| `nano [file]` | সহজ টার্মিনাল টেক্সট এডিটর দিয়ে ফাইল ওপেন/এডিট করে। | `nano script.sh` |
| `vim [file]` / `vi` | এডভান্সড টেক্সট এডিটর দিয়ে ফাইল ওপেন/এডিট করে। | `vim config.conf` |
| `grep "[text]" [file]` | ফাইলের ভিতর নির্দিষ্ট কোনো শব্দ বা লাইন খুঁজে বের করে। | `grep "error" log.txt` |

---

##  ৩. সিস্টেম ও পারফরম্যান্স দেখার কমান্ড (System Information)

| Command | Definition / কাজ | Example / উদাহরণ |
| :--- | :--- | :--- |
| `uname -a` | লিনাক্স কার্নেল ও সিস্টেমের সম্পূর্ণ তথ্য দেখায়। | `uname -a` |
| `top` | রিয়েল-টাইমে CPU, RAM এবং প্রসেস ব্যবহারে তালিকা দেখায়। | `top` |
| `htop` | `top`-এর সুন্দর ও কালারফুল ইন্টারফেস (ইনস্টল থাকতে হবে)। | `htop` |
| `df -h` | **Disk Free:** হার্ডডিক্সের ফাঁকা জায়গা মানুষের পাঠযোগ্য ফরম্যাটে (GB/MB) দেখায়। | `df -h` |
| `du -sh [dir]` | **Disk Usage:** নির্দিষ্ট ফোল্ডার কতটুকু জায়গা দখল করে আছে তা দেখায়। | `du -sh Downloads` |
| `free -m` | RAM-এর কতটুকু ব্যবহৃত ও ফাঁকা আছে তা Megabyte-এ দেখায়। | `free -m` |
| `uptime` | সিস্টেম কতক্ষণ ধরে চালু আছে তা দেখায়। | `uptime` |
| `whoami` | আপনি কোন ইউজার অ্যাকাউন্টে লগইন আছেন তা দেখায়। | `whoami` |

---

##  ৪. ফাইল পারমিশন ও ইউজার ম্যানেজমেন্ট (Permissions & Users)

| Command | Definition / কাজ | Example / উদাহরণ |
| :--- | :--- | :--- |
| `sudo [command]` | Superuser (রুট) প্রিভিলেজ নিয়ে কোনো কমান্ড এক্সিকিউট করে। | `sudo apt update` |
| `chmod [perms] [file]` | ফাইল বা ফোল্ডারের পারমিশন (Read/Write/Execute) পরিবর্তন করে। | `chmod +x script.sh` |
| `chown [user] [file]` | ফাইল বা ফোল্ডারের মালিকানা (Ownership) পরিবর্তন করে। | `chown root file.txt` |
| `useradd [user]` | নতুন ইউজার তৈরি করে। | `sudo useradd rahim` |
| `passwd [user]` | ইউজারের পাসওয়ার্ড তৈরি বা পরিবর্তন করে। | `sudo passwd rahim` |

---

##  ৫. নেটওয়ার্কিং কমান্ড (Networking Commands)

| Command | Definition / কাজ | Example / উদাহরণ |
| :--- | :--- | :--- |
| `ping [host]` | কোনো সার্ভার বা ওয়েবসাইটের কানেকশন টেস্ট করে। | `ping google.com` |
| `ip a` / `ifconfig` | ডিভাইসের IP Address এবং নেটওয়ার্ক ইন্টারফেসের তথ্য দেখায়। | `ip a` |
| `curl [url]` | ওয়েবসাইটের ডাটা বা API থেকে ডাটা ডাউনলোডের/দেখার কাজ করে। | `curl https://example.com` |
| `wget [url]` | ইন্টারনেট থেকে ফাইল সরাসরি ডাউনলোড করে। | `wget https://example.com/file.zip` |
| `netstat -tuln` | সিস্টেমে চালু থাকা পোর্টগুলোর তথ্য দেখায়। | `netstat -tuln` |
| `ssh [user]@[host]` | রিমোট সার্ভারে কানেক্ট করার জন্য ব্যবহৃত হয়। | `ssh user@192.168.1.1` |

---

##  ৬. প্যাকেজ ম্যানেজমেন্ট (Software Installation)

> **নোট:** Ubuntu/Debian ভিত্তিক সিস্টেমে `apt` ব্যবহার করা হয়। RedHat/CentOS-এ `yum` বা `dnf` ব্যবহার করা হয়।

| Command | Definition / কাজ | Example / উদাহরণ |
| :--- | :--- | :--- |
| `sudo apt update` | প্যাকেজ লিস্ট আপডেট করে। | `sudo apt update` |
| `sudo apt upgrade` | ইনস্টল করা সফ্টওয়্যারগুলো আপডেট করে। | `sudo apt upgrade` |
| `sudo apt install [pkg]` | নতুন কোনো প্রোগ্রাম বা সফটওয়্যার ইনস্টল করে। | `sudo apt install git` |
| `sudo apt remove [pkg]` | ইনস্টল করা কোনো সফ্টওয়্যার আনইনস্টল করে। | `sudo apt remove git` |

---

##  ৭. অন্যান্য কাজের কমান্ড (Miscellaneous)

| Command | Definition / কাজ | Example / উদাহরণ |
| :--- | :--- | :--- |
| `clear` | টার্মিনালের স্ক্রিন সাফ (Clear) করে। | `clear` |
| `history` | পূর্বে ব্যবহৃত কমান্ডগুলোর হিস্ট্রি বা তালিকা দেখায়। | `history` |
| `alias` | বড় কোনো কমান্ডের শর্টকাট তৈরি করতে ব্যবহৃত হয়। | `alias cls='clear'` |
| `man [command]` | **Manual:** যেকোনো কমান্ডের অফিসিয়াল নির্দেশিকা ও ব্যবহারের নিয়ম দেখায়। | `man ls` |
| `exit` | টার্মিনাল সেশন বন্ধ করে বের হয়ে যায়। | `exit` |