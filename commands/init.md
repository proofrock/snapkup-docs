# 📖 Init

#### Syntax

```
snapkup -d somedir init
```

#### Aliases

No aliases for this command.

#### Description

Initializes the folder _somedir _so that it can contain the backup files. The folder must be completely empty, not even containing .dotfiles or other hidden files.

Inside it, it will create 16 directories (`0/` to `f/`) and a file that will contain all the stored metadata, named `snapkup.dat`.

The directories will store the backup "blobs", whose name is a 128-bit hex string (e.g. `75daa5abb0e6bc0861b38a99a23fecd7`). In order not to put them at the same level, easily creating a folder with several thousands of files, snapkup will put them evenly into the directories.

Everything (`snapkup.dat` and the blobs) is compressed (if compressible) and encrypted.
