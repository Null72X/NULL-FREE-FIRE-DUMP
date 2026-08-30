# NULL-FREE-FIRE-DUMP

A comprehensive reverse-engineering toolkit and guide designed to extract, dump, and reconstruct the `libil2cpp.so` binary and `global-metadata.dat` files from Garena Free Fire. This project supports both ARMv7 (32-bit) and ARM64-v8a (64-bit) architectures and is intended for security research, modding, and structural analysis.

---

## 🚀 Key Features

* **Dual Extraction Strategies**:
  * **CRC Bypass Method (via CRCMainP)**: Bypasses file integrity checks by patching a placeholder `libmain.so` with the game's actual CRC32 checksum, forcing the game to generate automated memory dumps on boot.
  * **Game Guardian (GG) Memory Dumping**: Uses custom Lua scripts to dump binaries directly from running process memory, bypassing static protection and obfuscation.
* **Obfuscation & Header Recovery**:
  * Auto-locates metadata boundaries in memory using string table signature checks (e.g., searching for `mscorlib.dll` and `get_fieldOfView`).
  * Repairs obfuscated metadata headers automatically (verifies and rewrites the standard `0xFAB11BAF` magic number).
* **C# Structure Reconstruction**: Includes pre-configured `Il2CppDumper` binaries to parse the dumped binary and metadata into clean, readable C# prototype headers, class structures, and JSON offset maps.
* **Pre-bundled Dependencies**: Includes setup binaries for rooted emulators, file managers (`MT Manager`), and debugging tools.

---

## 🛠️ Tech Stack & Dependencies

* **Scripting**: Lua (for Game Guardian runtime memory manipulation)
* **Binary Modification Tools**: C++ & Qt4 (used in the `CRCMainP` checksum patching utility)
* **Reconstruction Engine**: C# / .NET (for `Il2CppDumper`)
* **Target Architectures**: Android ARMv7 (32-bit) & ARM64-v8a (64-bit)
* **Testing Environment**: Rooted BlueStacks Emulator (v5.12+ recommended)

---

## 📦 Project Structure

```directory
NULL-FREE-FIRE-DUMP/
├── Free Fire Dump CRC Method/       # Method 1: CRC Checksum patching method
│   ├── CRCMainP/                    # CRCMainP GUI & CLI patchers with Qt libraries
│   ├── Fake lib/                    # Pre-compiled fake libraries (armeabi-v7a & arm64-v8a)
│   └── Free Fire Dump Guide.txt     # Text guide for CRC method
├── Free Fire Dump GG Method/        # Method 2: Game Guardian memory script method
│   ├── Il2CppDumper/                # C# IL2CPP recovery utility
│   ├── LibDumper.lua                # Game Guardian script to dump libil2cpp.so & metadata
│   ├── Metadata Searcher.lua        # Game Guardian script to search obfuscated headers
│   ├── Free Fire Method 1 Guide.txt # Standard GG dumping guide
│   └── Free Fire Method 2 Guide.txt # Advanced signature-based GG dumping guide
├── Bluestacks-App-Player-*.exe      # Android Emulator Installer
├── Game-Guardian.apk                # Game Guardian memory modifier APK
├── MT-Manager.apk                   # Android file manager / editor APK
├── Root-Checker.apk                 # Emulator root validation utility
└── README.md                        # Project documentation (this file)
```

---

## ⚙️ Installation & Setup

### 1. Emulator Preparation
1. Run and install the provided **BlueStacks App Player** (`Bluestacks-App-Player-5-12-115-1001.exe`).
2. Root the BlueStacks emulator (use BSTweaker or enable root permissions via BlueStacks settings).
3. Install the following APKs (drag and drop into the emulator):
   * `Root-Checker.apk` (verify root access)
   * `MT-Manager.apk` (file management and property analysis)
   * `Game-Guardian.apk` (process memory access)

---

## 📖 Usage Guide

### Method A: CRC Bypass Method (CRCMainP)

This method patches a placeholder library to match the game's file hash, forcing the game to drop an unencrypted dump upon launch.

1. **Get the original CRC32 checksum**:
   * Open **MT Manager** on the emulator and navigate to:
     `/data/app/com.dts.freefireth-1/lib/arm/` (or equivalent package path).
   * Long-press `libmain.so`, open **Properties**, and copy the **CRC32** checksum value.
2. **Patch the fake library**:
   * Launch `crcmainp-gui.exe` inside the `Free Fire Dump CRC Method/CRCMainP` directory on your PC.
   * Under **Input Path**, load the corresponding fake `libmain.so` from the `Fake lib` directory:
     * `armeabi-v7a/libmain.so` for 32-bit.
     * `arm64-v8a/libmain.so` for 64-bit.
   * Input the copied CRC32 checksum and click **Patch**. A patched `libmain.so` will be generated in the tool folder.
3. **Deploy & Dump**:
   * Rename the emulator's original library file:
     `libmain.so` $\rightarrow$ `librealmain.so`
   * Move your patched `libmain.so` into the emulator's library directory.
   * Launch **Free Fire** 1–2 times. The game will dump metadata to:
     `/storage/emulated/0/Android/data/com.dts.freefireth/`
4. **Restore**:
   * Delete the patched `libmain.so` and rename `librealmain.so` back to `libmain.so`.

---

### Method B: Game Guardian Live Memory Dump

Ideal for games with dynamic decryption or heavily obfuscated binaries.

#### Option 1: Standard Dump
1. Run **Free Fire** and wait for the main login screen.
2. Open **Game Guardian**, select the Free Fire process, and execute `LibDumper.lua`.
3. Choose **Dump global-metadata.dat** and save it.
4. Execute `LibDumper.lua` again, select **Dump libil2cpp.so**, and select **Method 2** (memory-based dump) by sliding the configuration bar.
5. Export both generated files to your PC.

#### Option 2: Obfuscated/Hidden Metadata Dump
1. Launch **Free Fire** to the login screen.
2. Select the game process in **Game Guardian** and execute `Metadata Searcher.lua`.
3. If the metadata header is obscured, copy the signature address displayed by the script.
4. Replace the target value with the hexadecimal array `AF 1B B1 FA r`.
5. Navigate to the Memory Dump tab in Game Guardian, enter the copied address range in both **From** and **To** fields, select the size, and save the binary block.
6. Rename the exported `.bin` file to `global-metadata.dat`.
7. Execute `LibDumper.lua` to dump the obfuscated `libil2cpp.so` file using **Method 2**.

---

## 🔍 Restoring Code with Il2CppDumper

Once you have acquired the memory-dumped `libil2cpp.so` and `global-metadata.dat` files, use the bundled `Il2CppDumper` to reconstruct the game structures:

1. Launch `Il2CppDumper.exe`.
2. Select the dumped `(start address- <address>) libil2cpp.so` file.
3. Select the dumped `global-metadata.dat` file.
4. When prompted by the console, enter the `<address>` prefix parsed from the library file's name (e.g. if the filename is `(start address- 7b2c000000)libil2cpp.so`, enter `7b2c000000`).
5. Press **Enter** and allow the parsing process to complete.
6. Retrieve your C# structures, class files, and dump offsets inside the `Il2CppDumper` output directory.
