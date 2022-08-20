Restic wrapper
====

Restic documentation: https://restic.readthedocs.io/en/stable/010_introduction.html

This is simply a wrapper to make restic easier to use. Its usage is intended to an initialized restic repository.
See [here](https://restic.readthedocs.io/en/latest/030_preparing_a_new_repo.html) hot to initialize new repository.

To use this wrapper you have to configure two things: at least one `namespace` and `password` file path.

### Namespace
Namespace is made-up from three variables that contains three paths:
* `exclude_<repo_name>` - The path to the `.txt` file that contains the restic repo password.
* `repo_<repo_name>` - The path to the destination folder (The one initialized with the restic repo).
* `host_<repo_name>` - The source folder.

Example:

```bash
exclude_documents=~/Documents/excludes_documents.txt
repo_documents=/mnt/Synology/Home/Backup/Documents
host_documents=~/Documents
```
Note that the namespace is the `documents` suffix

### Password

Currently, this wrapper assumes that each repository relies on same password. So you just have to edit
the `PWD_FILE` variable. 

Example:

```bash
PWD_FILE~/Documents/restic/resticp.txt
```

### Available commands

Create a snapshot
```bash
restic-backups backup <namespace>
```
Delete old snapshots except last ${KEEP_LAST} (deleting data as well)
```bash
restic-backups prune <namespace>
```
Delete a specific snapshot (also deleting the data)
```bash
restic-backups prune_single <hash_snapshot>
```
List snapshots
```bash
restic-backups snapshots <namespace>
```
Restore a snapshot
```bash
restic-backups restore <namespace> <hash_snapshot> /destination/folder
```
