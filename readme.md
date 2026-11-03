# Ubuntu Disk Cleanup Guide

### 1. Check Current Disk Usage

Run this to see which partitions are full:

```bash
df -h
```

### 2. Clean Package Manager Cache

Remove downloaded `.deb` files and old package versions that are no longer needed:

```bash
sudo apt-get clean
sudo apt-get autoclean
```

### 3. Remove Unused Dependencies

Delete orphaned software packages left behind after uninstalling programs:

```bash
sudo apt-get autoremove -y
```

### 4. Trim System Logs (Journalctl)

Check how much space logs are taking:

```bash
journalctl --disk-usage
```

Keep only the last 3 days of logs:

```bash
sudo journalctl --vacuum-time=3d
```

Or cap the logs to a specific maximum size (e.g., 300MB):

```bash
sudo journalctl --vacuum-size=300M
```

### 5. Clear User Cache & Trash

Clear local user thumbnail and app caches:

```bash
rm -rf ~/.cache/thumbnails/*
```

Empty the trash bin permanently:

```bash
rm -rf ~/.local/share/Trash/*
```

---

## Find Large Files and Folders

If you still need to free up more space, use these commands to locate heavy files.

List top-level directories by size in the root folder:

```bash
sudo du -h --max-depth=1 / | sort -hr
```

Find files larger than 50MB across the system:

```bash
sudo find / -type f -size +50M -exec ls -lh {} +
```
