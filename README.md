# onefile - Combine Files for AI-Assisted Development

**onefile** is a command-line tool designed to streamline the process of preparing input for large language models (LLMs) in the context of AI-assisted development.  It's intended for use in interactive LLMs chat sessions to create tailored outputs for development purposes, offering increased flexibility compared to some AI integrated code editors.  By combining files of specific extensions from multiple directories into a single output file, you can tailor the context provided to your LLM.  This tool is particularly useful when working with newer LLMs that have large context windows, allowing you to easily provide various relevant files and code snippets in one place without the limitations inherent in some AI-integrated code editors.

## Installation

The recommended way to install `onefile` is via the Debian package.  This package is compatible with Debian 12 (Bookworm) and Ubuntu 22.04 (Jammy) and later.

1. **Download the package:**  Download the `.deb` package from the relevant repository.  (e.g., `onefile_1.0.0.deb`).
2. **Install:** Open a terminal and run the following command:

```bash
sudo dpkg -i onefile_1.0.0.deb
```
   * **Important:** If you encounter errors, verify that the dependencies listed in `DEBIAN/control` are properly installed and check your system permissions.

3. **Update (for future versions):** To update to a later version, download the newer `.deb` package and run:

```bash
sudo dpkg -i onefile_1.0.1.deb
```

This will replace the older version.  If `onefile` is already installed, you can remove the current version with:
```bash
sudo apt remove onefile
```

## Usage

```bash
onefile [OPTIONS]
```

**Options:**

* **`-d`, `--directories` <dir1>[,<dir2>...]**: Comma-separated list of directories to search.  Defaults to the current directory (`.`).  For example, `-d src,lib,tests`.
* **`-e`, `--extensions` <ext1>[,<ext2>...]**: Comma-separated list of file extensions to combine.  If not specified, all files are included, *except* for those excluded (using `-x`).  Example: `-e js,ts`.
* **`-x`, `--exclude` <exclude1>[,<exclude2>...]**: Comma-separated list of directories to exclude from the search.  This is useful for ignoring directories like `node_modules`, `.git`, or temporary folders.  For example: `-x node_modules,.git`.
* **`-o`, `--output` <output_file>**: Specify the output file.  Defaults to `output_combined_files.txt`.  Example: `-o combined_files.txt`.
* **`-h`, `--header` <header>**: Add a header to the output file.  The content of the header should be provided after this flag.  Example: `-h "My Project Files - Version 1.0"`.
* **`-s`, `--silent`**: Suppress printing of relative file paths to the terminal during processing.  This option is useful for making the output less verbose.
* **`-a`, `--append`**: Append to the output file instead of overwriting it.  Useful for accumulating files over time.
* **`-y`, `--yes`**: Skip the confirmation prompt before writing files.  This is typically used in automated scripts.
* **`-p`, `--print`**: Always print relative file paths to the terminal, even without the prompt.
* **`-v`, `--version`**: Print the version number of onefile and exit.

## Examples

* **Combine JavaScript and TypeScript files from the current directory, excluding `node_modules`, into `combined.js`:**

```bash
onefile -d . -e js,ts -x node_modules -o combined.js
```

* **Combine all files in `src` and `lib`, add a header, and suppress path printing into `project_files.txt`:**

```bash
onefile -d src,lib -h "My Project Files - All Files" -s -o project_files.txt
```

* **Append Python files from `scripts` to `existing_code.py`, skipping confirmation:**

```bash
onefile -d scripts -e py -a -o existing_code.py -y
```

* **Print the version number:**

```bash
onefile -v
```

## Error Handling

If `onefile` encounters an error, it will print an error message to the standard error stream (`stderr`).  Here are some common issues:


* **Directory not found:** The specified directory does not exist.
* **File not found:** One or more files that `onefile` tries to process are missing.
* **Permission denied:** You do not have sufficient permissions to read or write the files.
* **Invalid option:** An incorrect option was used.
    *  Verify the `onefile` command syntax for correct usage.

## Important Considerations

* **File Paths:** The utility processes files using relative paths to the directories specified with `-d`.  Be very careful with the directory structure when using the `-d` option, especially if you're trying to combine files from different subfolders.
* **Relative Paths:** `onefile` uses relative paths, so the directory structure is important.  Be careful about how files are nested.
* **Large Files:**  Processing many large files might take time.
* **Confirmation Prompts:**  The prompts are designed to prevent accidental overwrites.
* **Permissions:** Ensure appropriate permissions when running `onefile`.

## Reporting Bugs/Issues

If you encounter a problem, please provide the following information:

* **Command used.**
* **Error output.**
* **Expected behaviour.**
* **onefile version and your operating system.**
* **Any relevant details about your file structure.**

## Contributing

Contributions are welcome.  See [link to contribution guidelines](link_to_contributing_guide).
