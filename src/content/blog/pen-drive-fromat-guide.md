---
author: Ash
pubDatetime: 2025-06-21T1:20:00Z
title: How to Format a Write-Protected USB on Windows
postSlug: Troubleshoot
featured: true
draft: false
tags:
  - troubleshooting
ogImage: ""
description: How to Format a Write-Protected  USB on Windows
---

## 🧹 How to Format a Write-Protected USB on Windows

If you've flashed Linux Mint on a pen drive and it's now **write-protected** or not formatting on Windows, follow this step-by-step guide.

---

## 🔍 Step 1: Check for Physical Lock

Some USB drives have a **tiny lock switch**. Make sure it's **not in the "Lock" position**.

---

## 💻 Step 2: Use `diskpart` in Windows

1. Open **Run** (`Win + R`) → type `diskpart` → hit **Enter**
2. Run the following commands:

```bash
list disk
select disk 1         # Replace with the correct disk number
attributes disk clear readonly
clean
create partition primary
list volume #Find the volume corresponding to your Disk 1 (in my case for ~14GB).
select volume X   ← replace X with your volume number
format fs=fat32 quick
assign
exit
```
