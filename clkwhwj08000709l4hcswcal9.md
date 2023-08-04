---
title: "🐧 Linux Troubleshooting Scenarios 🐧"
datePublished: Fri Aug 04 2023 11:21:21 GMT+0000 (Coordinated Universal Time)
cuid: clkwhwj08000709l4hcswcal9
slug: linux-troubleshooting-scenarios
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691148008832/b35c8a0f-f331-4053-be96-1e245fc8a12f.jpeg
tags: linux, linux-commands, 90daysofdevops

---

When it comes to troubleshooting on Unix/Linux systems, having the right approach is key. Whether you're a Software Developer, DevOps Engineer, or Architect, understanding the problems and their resolutions is vital in this widespread environment.

Let's dive into some common scenarios and their solutions:

### **Issue 1: Server Connectivity Problem** 🔍 **Approach / Solution**:

* ✅ Ping server by Hostname and IP Address.
    
* ✅ Check if Hostname/IP Address is pingable.
    
    * ❗ If only IP is pingable, it might be a DNS issue.
        
        * 📌 Check `/etc/hosts`, `/etc/resolv.conf`, and `/etc/nsswitch.conf`.
            
        * 📌 Optionally, check DNS in `/etc/sysconfig/network-scripts/ifcfg-<interface>`.
            
    * ❗ If neither is pingable, investigate network side or server-specific problems.
        
        * 📋 Check uptime, IP status, routes, Selinux, and Firewall rules.
            
        * 🔌 Examine physical cable connections.
            

### **Issue 2: Unable to Connect to Website/Application** 🔍 **Approach / Solution**:

* ✅ Ping server by Hostname and IP Address.
    
* ❗ If pingable, use telnet to check service availability.
    
    * ✅ If service is running, inspect firewall, logs, and configuration.
        

### **Issue 3: Unable to SSH** 🔍 **Approach / Solution**:

* ✅ Ping server by Hostname and IP Address.
    
* ❗ If pingable, use telnet to check service availability.
    
    * ✅ If service is running, verify user status, shell, and root login.
        
* 📋 Check service status, firewall, logs, and configuration.
    

### **Issue 4: Full Disk Space or Disk Extension** 🔍 **Approach / Solution**:

* ✅ Detect system performance degradation.
    
* ❗ Identify space issues with `df` and find large files with `du`.
    
    * 🗜 Compress/remove large files, move items, check disk health.
        
    * 📁 Add new disk, create partitions (LVM), extend filesystems.
        

### **Issue 5: Corrupted Filesystem** 🔍 **Approach / Solution**:

* ✅ Check logs for errors causing boot failure.
    
* ❗ Run `fsck` for bad sectors.
    
    * 🔧 Reboot into rescue mode, fix filesystem, edit `fstab` entries.
        

### **Issue 6: Fstab File Errors** 🔍 **Approach / Solution**:

* ✅ Check logs for boot errors.
    
* ❗ Run `fsck` for bad sectors.
    
    * 🔧 Reboot into rescue mode, fix filesystem, edit `fstab` entries.
        

### **Issue 7: Can't cd to Directory** 🔍 **Approach / Solution**:

* 📋 Check directory existence, path conflicts, permissions, and executability.
    

### **Issue 8: Can't Create Links** 🔍 **Approach / Solution**:

* 📋 Check target existence, path conflicts, permissions, ownership.
    

### **Issue 9: Running Out of Memory** 🔍 **Approach / Solution**:

* 📈 Monitor cache and RAM usage with commands like `free -h`.
    
* ❗ Identify memory-hungry processes, adjust priorities, extend swap space.
    

### **Issue 10: Add/Extend Swap Space** 🔍 **Approach / Solution**:

* ❗ Create swap file, set permissions, enable swap with `swapon`.
    
* 📋 Update `fstab` for persistence.
    

### **Issue 11: Unable to Run Commands** 🔍 **Approach / Solution**:

* ❗ Troubleshoot permission, sudo access, paths, installation issues.
    

### **Issue 12: Unexpected System Reboot and Process Restart** 🔍 **Approach / Solution**:

* 🔄 Investigate system crash reasons (CPU, RAM, kernel, hardware).
    
* 🔁 Understand process restart methods and watchdog applications.
    

### **Issue 13: Unable to Get IP Address** 🔍 **Approach / Solution**:

* 🔌 Check IP assignment methods (DHCP, Static).
    
* ❗ Troubleshoot network settings, NIC status, and restart network service.
    

### **Issue 14: Backup and Restore File Permissions** 🔍 **Approach / Solution**:

* 📋 Create ACL file before changing permissions, restore with `setfacl`.
    
* 📸 Consider VM snapshots or rebuilds for restoring permissions.
    

### 💡 **Useful Disk Partition Tip** 💡:

* 📊 Rescan new disk status with `echo 1 > /sys/block/sda/device/rescan`.
    
* 📝 Expanding existing disks appends space, doesn't affect existing data.
    
* 🔄 Recreate filesystems to format old data, share `.vmdk` for replication.
    

Mastering Linux troubleshooting helps ensure smooth operations and efficient problem-solving in your IT journey! 🚀🔧