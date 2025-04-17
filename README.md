# bulk-ext-renamer

A Python CLI tool to recursively rename all file extensions in a directory. For example, convert all `.jpeg` files to `.jpg` in nested folders.

## Features
- Recursive directory traversal
- Dry run mode
- Easy-to-use CLI

## Usage
```bash
python bulk_ext_renamer.py --src-dir ./images --old-ext .jpeg --new-ext .jpg

Requirements
Python 3.6+


### 🧠 `bulk_ext_renamer.py`
```python
import os
import argparse

def rename_extensions(src_dir, old_ext, new_ext, dry_run=False):
    for root, _, files in os.walk(src_dir):
        for file in files:
            if file.endswith(old_ext):
                old_path = os.path.join(root, file)
                new_path = os.path.join(root, file[:-len(old_ext)] + new_ext)
                print(f"{'[DRY RUN]' if dry_run else ''} Renaming: {old_path} -> {new_path}")
                if not dry_run:
                    os.rename(old_path, new_path)

if __name__ == "__main__":
    parser = argparse.ArgumentParser()
    parser.add_argument("--src-dir", required=True, help="Directory to scan")
    parser.add_argument("--old-ext", required=True, help="Old file extension (e.g. .jpeg)")
    parser.add_argument("--new-ext", required=True, help="New file extension (e.g. .jpg)")
    parser.add_argument("--dry-run", action="store_true", help="Simulate renaming")
    args = parser.parse_args()

    rename_extensions(args.src_dir, args.old_ext, args.new_ext, args.dry_run)
