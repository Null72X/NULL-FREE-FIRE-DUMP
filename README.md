# Free Fire libmain.so Dump Guide

<div align="center">

### Owner: NULL
### Created By: Gaurav

</div>

---

## 📖 Overview

This repository contains a guide for dumping `libmain.so` using a rooted BlueStacks emulator, MT Manager, and CRCMainP GUI.

> ⚠️ This guide is provided for educational and research purposes only.

---

## 📋 Requirements

Before starting, make sure you have the following:

- Rooted BlueStacks Emulator
- MT Manager
- CRCMainP GUI (`crcmainp-gui.exe`)
- Fake `libmain.so` (32-bit or 64-bit)
- Free Fire installed

---

# 🚀 Step 1: Set Up the Emulator

1. Launch a rooted BlueStacks emulator.
2. Install MT Manager.
3. Grant all required permissions.
4. Verify root access is working properly.

---

# 🔍 Step 2: Obtain the CRC32

### Navigate to:

```text
/data/app/com.dts.freefireth-1/lib/arm/
```

### Instructions

1. Open MT Manager.
2. Locate `libmain.so`.
3. Open **Properties**.
4. Find the **Checksum** section.
5. Copy the **CRC32** value.

---

# 🛠️ Step 3: Patch the Fake Library

1. Open the CRCMainP folder on your PC.
2. Run:

```text
crcmainp-gui.exe
```

3. Click **Input Path**.
4. Select the appropriate fake `libmain.so`:

| Architecture | Version |
|-------------|----------|
| 32-bit | armeabi-v7a |
| 64-bit | arm64-v8a |

5. Paste the copied CRC32 into the CRC32 field.
6. Click **Patch**.

### Result

A new file named:

```text
libmain.so
```

will be generated inside the CRCMainP folder.

---

# 📦 Step 4: Replace the Original File

Transfer the newly generated `libmain.so` to the emulator.

### Navigate to:

```text
/data/app/com.dts.freefireth-1/lib/arm/
```

### Backup the Original Library

Rename:

```text
libmain.so
```

to:

```text
librealmain.so
```

### Copy the Patched Library

Move the patched:

```text
libmain.so
```

into the same directory.

---

# 🎯 Step 5: Generate the Dump

1. Launch Free Fire.
2. Open the game 1–2 times.
3. Wait for the dump process to complete.

### Dump Output Location

```text
/storage/emulated/0/Android/data/com.dts.freefireth/
```

The generated dump file should appear in the directory above.

---

# ♻️ Step 6: Restore the Original Library

After dumping is complete:

### Delete the Patched Library

```text
libmain.so
```

### Restore the Backup

Rename:

```text
librealmain.so
```

back to:

```text
libmain.so
```

### Verify

Ensure the original library has been restored successfully.

---

# 📂 Important Paths

## Original Library

```text
/data/app/com.dts.freefireth-1/lib/arm/libmain.so
```

## Dump Output

```text
/storage/emulated/0/Android/data/com.dts.freefireth/
```

---

# ⚠️ Notes

- Use the correct architecture version (32-bit or 64-bit).
- Always keep a backup of the original `libmain.so`.
- Root access is required.
- Verify the CRC32 value before patching.
- If no dump is generated, repeat the process and check all steps carefully.

---

# 🛠️ Troubleshooting

### No Dump Generated

Possible causes:

- Incorrect CRC32 value
- Wrong architecture selected
- File not copied correctly
- Missing root permissions

### Game Crashes

Possible causes:

- Invalid patched library
- Wrong architecture version
- Corrupted file transfer

Restore the original `libmain.so` and try again.

---

# 👤 Credits

### Created By
**Gaurav**

### Owner
**NULL**

---

<div align="center">

⭐ If you found this repository useful, consider starring it.

</div>
