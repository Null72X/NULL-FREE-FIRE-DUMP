# Free Fire libmain.so Dump Guide

A step-by-step guide for dumping `libmain.so` using a rooted BlueStacks emulator, MT Manager, and CRCMainP GUI.

> ⚠️ Educational and research purposes only. Ensure you comply with the game's Terms of Service and applicable laws.

---

## 📋 Requirements

Before starting, make sure you have:

- Rooted BlueStacks Emulator
- MT Manager
- CRCMainP GUI (`crcmainp-gui.exe`)
- Fake `libmain.so` (32-bit or 64-bit version)
- Free Fire installed

---

## 🚀 Step 1 — Set Up the Emulator

1. Launch a **rooted BlueStacks emulator**.
2. Install **MT Manager**.
3. Grant all requested permissions.
4. Verify root access is working properly.

---

## 🔍 Step 2 — Obtain the CRC32

### Navigate to:

```text
/data/app/com.dts.freefireth-1/lib/arm/
```

### Instructions

1. Open **MT Manager**.
2. Locate **libmain.so**.
3. Tap **Properties**.
4. Find the **Checksum** section.
5. Copy the **CRC32** value.

---

## 🛠️ Step 3 — Patch the Fake Library

1. Open the **CRCMainP** folder on your PC.
2. Run:

```text
crcmainp-gui.exe
```

3. Click **Input Path**.
4. Select the correct fake `libmain.so`:

| Architecture | File |
|-------------|------|
| 32-bit | armeabi-v7a |
| 64-bit | arm64-v8a |

5. Paste the copied **CRC32** into the CRC32 field.
6. Click **Patch**.

### Result

A new file named:

```text
libmain.so
```

will be generated inside the **crcmainp** folder.

---

## 📦 Step 4 — Replace the Original File

Transfer the newly generated `libmain.so` to the emulator.

### Navigate to:

```text
/data/app/com.dts.freefireth-1/lib/arm/
```

### Backup Original File

Rename:

```text
libmain.so
```

to:

```text
librealmain.so
```

### Copy Patched File

Move the patched:

```text
libmain.so
```

into the same directory.

---

## 🎯 Step 5 — Generate the Dump

1. Launch **Free Fire**.
2. Open the game **1–2 times**.
3. Wait for the dumping process to finish.

### Dump Location

```text
/storage/emulated/0/Android/data/com.dts.freefireth/
```

If successful, the dump file will appear in the directory above.

---

## ♻️ Step 6 — Restore the Original Library

After dumping is complete:

### Delete Patched File

```text
libmain.so
```

### Restore Backup

Rename:

```text
librealmain.so
```

back to:

```text
libmain.so
```

### Verify

Ensure the original library has been restored successfully before launching the game again.

---

## 📂 Directory References

### Original Library

```text
/data/app/com.dts.freefireth-1/lib/arm/libmain.so
```

### Dump Output

```text
/storage/emulated/0/Android/data/com.dts.freefireth/
```

---

## ⚠️ Notes

- Use the correct architecture version (**32-bit** or **64-bit**).
- Always create a backup before replacing any game files.
- Root access is required.
- Verify the CRC32 value is copied correctly.
- If no dump is generated, repeat the patching process and double-check the CRC32.

---

## 📝 Troubleshooting

### Dump Not Generated

Possible causes:

- Incorrect CRC32 value
- Wrong architecture selected
- Patched file not copied correctly
- Root permissions not granted
- Game not launched after replacement

### Game Crashes

Possible causes:

- Invalid patched library
- Wrong architecture version
- Corrupted file transfer

Restore the original `libmain.so` and try again.

---

## ⭐ Credits

- MT Manager
- BlueStacks
- CRCMainP

If this guide helped you, consider starring the repository.
