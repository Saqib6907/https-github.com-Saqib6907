# 🖥️ How I Fixed the Black Box on Windows Desktop Icons

If you've ever been greeted by strange black boxes behind your desktop icons, you're not alone. I recently faced this frustrating issue—along with deeper system file corruption—and after trying multiple fixes, I finally found a reliable solution. Here's how I did it, step by step.

---

## 🔍 The Problem

It started with black boxes appearing behind my desktop icons. I suspected it was related to a corrupted IconCache or deeper system issues. I tried clearing the cache and restarting Explorer, but the problem persisted. So I rolled up my sleeves and went deeper.

---

## 🛠️ Step-by-Step Fix

### 1. **Run System File Checker (SFC)**
I opened **Command Prompt as Administrator** and ran:
```
sfc /scannow
```
This scanned my system for corrupted files. It found issues—but couldn’t fix everything.

### 2. **Run DISM to Repair the Windows Image**
Next, I ran:
```
DISM /Online /Cleanup-Image /RestoreHealth
```
Unfortunately, DISM failed a couple of times. That meant my system image was too damaged for online repair.

### 3. **Download Windows ISO and Perform In-Place Upgrade**
I downloaded the official Windows ISO from [Microsoft’s website](https://www.microsoft.com/software-download/windows10), mounted it, and ran `setup.exe`.

- I chose **“Keep personal files and apps”** during setup.
- This refreshed my system files without wiping my data.

### 4. **Run SFC Again**
After the upgrade, I ran `sfc /scannow` once more. This time, it successfully repaired the remaining corrupted files:
> *Windows Resource Protection found corrupt files and successfully repaired them.*

Victory.

---

## 🧹 Optional Cleanup Steps

To make sure everything was clean and stable, I also did the following:

- **Deleted IconCache manually**:  
  `C:\Users\<YourUsername>\AppData\Local\IconCache.db`  
  Then restarted my PC.

- **Ran Disk Cleanup**:  
  Cleared thumbnail cache and temporary files.

- **Created a Restore Point**:  
  So I could roll back to this clean state if needed.

---

## 💡 Final Thoughts

This layered approach—SFC, DISM, ISO setup—worked like a charm. If you're facing similar icon glitches or system corruption, I highly recommend following these steps. It’s a clean recovery path that doesn’t require wiping your system.

If you're a developer or tech enthusiast like me, you might even consider building a small utility to automate these checks. In sha Allah I’m exploring that next in C#.

---
