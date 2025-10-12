---
id: user-guide
title: User Guide
sidebar_position: 3
---

# 7-ZIP User Guide
7-Zip is a free and open-source file archiver designed for high compression efficiency and broad file format support. Whether you're looking to compress large folders, extract archived files, or secure your data with encryption, 7-Zip offers a lightweight and powerful solution.

## Key Features
- High compression ratio using 7z format

- Support for a wide range of archive formats (ZIP, RAR, TAR, GZIP, and more)

- Integration with Windows context menu

- Password-protected and encrypted archives

- Multi-part (split) archive creation

- Command-line support for automation and scripting

## Who This Guide Is For
- New users wanting to learn how to extract or compress files

- Power users looking for advanced features like split archives or CLI tools

- Anyone seeking a free, fast, and reliable alternative to commercial archivers

By the end of this guide, you'll be able to confidently install 7-Zip, navigate its interface, and perform common file archiving tasks with ease.

***
  ## Installation Guide

**1. Download 7-Zip**

Visit the official [7-Zip website](https://www.7-zip.org/) and choose the correct version for your system:
* 64-bit Windows – most common.
* 32-bit Windows – for older systems.

**2. Run the Installer**

Double-click the downloaded `.exe` file and select **Yes** if prompted by User Account Control.

**3. Install the Program**

* Choose your installation folder (or keep the default) and select **Install**. 
* Select **Close** once installation completes.
* To verify the installation, locate 7-Zip on your desktop or **Start Menu** and run it.

## Basic Usage
Whether you're new to file compression or just getting started with 7-Zip, the following steps will help you perform common actions like extracting files, creating archives, and exploring archive contents using the 7-Zip File Manager. 

  ### How to Extract Files
Extracting files with 7-Zip is quick and easy. Follow these steps to unpack compressed files:

**Method 1: Using Right-Click Context Menu**

1. Open 7-Zip and locate the archive file (e.g., .zip, .7z, .rar).

2. Right-click the archive file.

3. Hover over the **7-Zip** in the menu.

4. Choose one of the following options:

   * **Extract files...** – lets you choose a destination and options before extracting.
   * **Extract Here** – extracts files to the current folder.
   * **Extract to "Folder Name"** – creates a new folder and extracts files into it.

![Extracting Files Through Context Menu](/img/1_Extract_01.png)

**Method 2: Using 7-Zip File Manager**

1. Open **7-Zip File Manager** from the Start Menu.

2. Navigate to the archive file and double-click to open it.

3. Select **Extract** on the toolbar.

4. Choose a destination folder in the pop-up window.

5. Select **OK** to begin extraction.

![Extracting FIles Throught File Manager](/img/1_Extract_02.png)

  ### How to Compress Files

7-Zip allows you to compress files and folders into archive formats like .7z or .zip, reducing file size and making sharing easier. Here's how to do it:

**Method 1: Using Right-Click Context Menu**

1. Select the file(s) or folder(s) you want to compress.

2. Right-click the selection.

3. Hover over the **7-Zip** in the menu.

4. Choose one of the following options:

   * **Add to archive...** – opens a settings window where you can customize format, compression level, password protection, and more.
   * **Add to "filename.7z"** – quickly compresses using default settings.
   * **Add to "filename.zip"** – creates a standard `.zip` archive for compatibility.

![Creating Archive Through Context Menu](/img/2_Archive_01.png)

**Method 2: Using 7-Zip File Manager**

1. Open 7-Zip File Manager.

2. Navigate to and select the desired files or folders.

3. Select the **Add** button on the toolbar.

4. Configure archive options:

   * **Archive format** – choose the archive format (`.7z`, `.zip`, etc.)
   * **Compression level** – choose from **0 - Store** (fastest) to **9 - Ultra** (smallest size).
   * Optional: Set a password for encrypted archive.

![Creating Archive Through File Manager](/img/2_Archive_02.png)

  ### Using Context Menu Options

7-Zip integrates directly into the Windows right-click (context) menu, making it easy to access common features without opening the 7-Zip File Manager. Here’s a guide to the most useful options:

**Right-Click Menu Overview**

When you right-click a file or folder, hover over **7-Zip** to reveal these common options:

| **Option** | **Description** |
|----------|---------------|
| **Open archive** | Opens the file in 7-Zip File Manager without extracting it. |
| **Extract files…** | Lets you choose a destination and extraction options before extracting. |
| **Extract Here** | Immediately extracts the contents of the archive to the current folder. |
| **Extract to "Folder Name"** | Creates a subfolder with the archive's name and extracts files into it. |
| **Add to archive…** | Opens a settings window to customize compression format, level, and other options. |
| **Add to "filename.7z" / "filename.zip"** | Quickly compresses files into a `.7z` or `.zip` archive using default settings. |
| **Compress and email…** | Compresses the file and attaches it to a new email (requires a configured email client). |

**Customizing Context Menu**

You can customize which options appear in the right-click menu by:

1. Opening 7-Zip File Manager.

2. Going to **Tools** > **Options**.

3. Under the **7-Zip** tab, check or uncheck context menu items.

## Advanced Features
While 7-Zip is well known for its simplicity, it also offers a range of advanced features for users who need more control over file compression and management. This chapter explores tools such as password protection, archive splitting, command-line operations, and format-specific options. These features allow for greater security, flexibility, and efficiency in handling large or sensitive files.

Whether you're a power user or just curious about what's under the hood, this section will help you get the most out of 7-Zip's capabilities.

  ### Split Archives
7-Zip allows you to split large archives into multiple smaller parts—ideal for transferring via email, USB drives, or systems with file size limits. Each part is labeled and can be rejoined automatically during extraction.

**How to Create a Split Archive**

1. Select the file(s) or folder(s) you want to compress.

2. Right-click the selection and choose **7-Zip** > **Add to archive...**.

3. In the **Add to Archive** window, under **Split to volumes, bytes**, enter a size for each part. 

- Examples:

   * `100M` for 100 megabytes
   * `700M` for CD-sized parts
   * `4G` for DVD-sized parts

4. Configure other settings as needed and select **OK** to start creating the split archive.

![Creating Split Archive](/img/3_Split Archives_01.png)

**Result**

7-Zip will generate multiple files with numbered extensions like:

```
archive.7z.001  
archive.7z.002  
archive.7z.003

```

**How to Extract Split Archives**

1. Make sure all parts (`.001`, `.002`, etc.) are in the same folder.

2. Right-click the `.001` file and choose **7-Zip** > **Extract Here** or another extraction option.

3. 7-Zip will automatically combine and extract the full archive.

![Extracting Split Archive](/img/3_Split Archives_02.png)

  ### Password Protection
7-Zip allows you to secure your compressed files with a password, helping protect sensitive data from unauthorized access. When you set a password, 7-Zip encrypts both the file contents and (optionally) the list of archived files.

**How to Create a Password-Protected Archive**

1. Select the file(s) or folder(s) to compress.

2. Right-click and choose **7-Zip** > **Add to archive...**.

3. In the **Add to Archive** window:

   * Scroll down to the **Encryption** section.
   * Enter your password in the **Enter password** and **Reenter password** fields.
   * (Recommended) Select the **Encrypt file names** checkbox to fully protect archive contents.

4. Select **OK** to create the encrypted archive.

![Encryption](/img/4_Encryption_01.png)

**Opening a Password-Protected Archive**

1. Double-click the archive or try to extract it.

2. When prompted, enter the correct password.

3. If the password is correct, the files will be accessible or extracted.

**Important Notes**

- Don't forget your password—7-Zip uses strong encryption (AES-256), and there's no way to recover files without it.
- Only the `.7z` format supports full encryption of file names.

  ### Command Line Options
For users who prefer automation, scripting, or working in a terminal environment, 7-Zip offers a full-featured command-line interface. This allows advanced control over compression, extraction, and file management tasks.

**Basic Syntax**

```
7z [command] [options] [archive_name] [files...]
```
| Element | Description |
|---------|-------------|
| `7z` | The command-line version of 7-Zip |
| `[command]` | The operation to perform (e.g., `a`, `x`, `e`) |
| `[options]` | Optional switches like compression level or password |
| `[files...]` | File(s) or folder(s) to compress or extract |

**Common Commands**

| Command | Description | Example |
|---------|-------------|---------|
| `a` | Add files to an archive | `7z a archive.7z file1.txt folder\` |
| `x` | Extract with full paths | `7z x archive.7z` |
| `e` | Extract without restoring folder structure | `7z e archive.zip` |
| `t` | Test archive integrity | `7z t archive.7z` |
| `l` | Test archive integrity | `List archive contents` |

**Useful Options**

- `p[password]` – Set a password

- `mhe=on` – Encrypt file names

- `mx=9` – Set compression level (0–9)

- `o[folder]` – Set output directory

- `v100m` – Split archive into 100MB parts

**Example: Create Encrypted Split Archive**

To create a password-protected, split archive from the Documents folder: 
```
7z a -pSecret123 -mhe=on -v100m secure.7z Documents\
```

  ### Format-specific Options
7-Zip supports several archive formats, each with its own strengths and customizable options. When creating archives, you can tailor settings depending on the format you choose—especially for `.7z`, `.zip`, and `.tar`.

**.7z Format**

The default and most feature-rich format in 7-Zip. Supports high compression and strong AES-256 encryption.

Key Options:
- Compression Level (`-mx`): 0 (none) to 9 (ultra)

- Compression Method: LZMA (default), LZMA2, PPMd, BZip2

- Solid Block Size (`-ms`): Groups similar files for better compression

- Encryption: AES-256 with file name encryption (`-mhe=on`)

Example:
```
7z a -t7z -mx=9 -mhe=on -pMyPass archive.7z files\
```

**.zip Format**

Widely supported and compatible with most systems. Best for sharing with users who don’t use 7-Zip.

Key Options:

- Compression Method: Deflate (default), BZip2, LZMA

- Encryption: ZipCrypto or AES-256 (not all tools support AES)

- Split Archives: Supported (e.g., `-v50m`)

Example:
```
7z a -tzip -pSecret123 -mem=AES256 archive.zip files\
```

**.tar Format (and .tar.gz / .tar.bz2)**

Common in Linux/Unix systems. TAR itself doesn’t compress - it packages files before applying compression (like GZip or BZip2).

Key Options:

Compression is applied in a second step

- `7z a archive.tar folder\`
- `7z a -tgzip archive.tar.gz archive.tar`

Note: Use this when you need compatibility with Linux tools.

## Troubleshooting
If you encounter issues while using 7-Zip, here are some common problems and solutions to help you resolve them quickly.

**1. "Cannot open file as archive"**

Cause: The file may be corrupted, incomplete, or not a valid archive.

Solutions:
* Make sure the download completed successfully.
* If it’s a split archive, ensure all parts (`.001`, `.002`, etc.) are in the same folder.
* Try opening the archive using 7-Zip File Manager instead of double-clicking.

**2. Archive asks for a password but you didn’t set one**

Cause: The file was encrypted by someone else.

Solutions:
* Contact the sender for the correct password.
* Without the correct password, the archive contents cannot be accessed or recovered.

**3. Right-click 7-Zip options missing**

Cause: Integration with the Windows context menu may be disabled.

Solutions:
* Open 7-Zip File Manager.
* Go to **Tools** > **Options** > **7-Zip** tab.
* Make sure the checkboxes for context menu options are selected, then select **Apply**.

**4. Can’t extract files from a split archive**

Cause: One or more parts of the archive are missing or renamed.

Solutions:
* Make sure all parts are in the same folder and correctly named (`.001`, `.002`, etc.).
* Start extraction from the `.001` file only.

**5. Compression is very slow**

Cause: High compression level or solid archive settings.

Solutions:
* Try a lower compression level (e.g., `-mx=5` instead of `-mx=9`).
* Avoid using solid mode for archives with many small, unrelated files.

## FAQ (Frequently Asked Questions)
**1. Is 7-Zip free to use?**

Yes. 7-Zip is completely free, open-source software. You can use it for personal or commercial purposes without any license fees.

**2. Which archive format should I use: .7z or .zip?**

- Use .7z for better compression and advanced features like strong encryption.
- Use .zip for maximum compatibility with other systems and users.

**3. Can I create self-extracting archives?**

Yes. In the **Add to Archive** window, select **Create SFX archive** to make a self-extracting `.exe` file that doesn’t require 7-Zip to unpack.

**4. How do I update or modify an existing archive?**

7-Zip does not support direct modification. You must extract the archive, make changes, and then re-compress the contents into a new archive.

**5. Is 7-Zip available on Linux or macOS?**

- On Linux, use the `p7zip` package (command-line version of 7-Zip).
- On macOS, 7-Zip isn't officially supported, but you can use third-party apps like **Keka** or install **p7zip** via Homebrew.

## Support and Resources
If you need more help or want to explore advanced topics beyond this guide, the following resources and support options are available:

**Official Resources**

- [7-Zip Official Website](https://www.7-zip.org/): Download the latest version, view release notes, and access official documentation.

- [7-Zip FAQ (Official)](https://www.7-zip.org/faq.html): Answers to technical questions and feature explanations.

**Community Support**

- [SourceForge Forums](https://sourceforge.net/p/sevenzip/discussion/): Community discussions, bug reports, and feature requests.

- Reddit & Stack Overflow: Search for "7-Zip" on platforms like [Reddit](https://www.reddit.com/r/software/) or [Stack Overflow](https://stackoverflow.com/questions/tagged/7zip) for user experiences, tips, and troubleshooting advice.

**Contacting Developers**

7-Zip is maintained by Igor Pavlov. There is no formal support team, but you can report bugs or suggestions via the [SourceForge project page](https://sourceforge.net/projects/sevenzip/).




