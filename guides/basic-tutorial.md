# 🔢 Basic tutorial

In this tutorial, we will back up the contents of the `/home/my/MyImportantDir`, using the `/home/my/MySnapkupDir` folder as the container of the backup structures.&#x20;

{% hint style="info" %}
All the commands have shortcuts; e.g. `root add` can be `r a`. Read the help! (`snapkup --help`)
{% endhint %}

{% hint style="info" %}
UNIX-style command is used (`snapkup`); of course, under windows you will use `snapkup.exe`
{% endhint %}

### Specify the encryption password

Everything is encrypted in snapkup, so you have to specify the password. There are three ways to do so: via an environment variable; via a credentials file in the filesystem; or via prompt in the application.

**From env var**

The encryption password can be read from an environment variable, `SNAPKUP_PASSWORD`, so you can use:

```
// UNIX
export SNAPKUP_PASSWORD=MyCoolPwd

// Windows CMD (batch files)
set "SNAPKUP_PASSWORD=MyCoolPwd"

// Windows Powershell
$env:SNAPKUP_PASSWORD = 'MyCoolPwd'
```

**From credentials file**

You can create a `.snapkup-creds` file in your home dir, and assign a password to a profile:

```
myProfile:MyCoolPwd
```

Then start snapkup specifying the profile:

```
snapkup --profile myProfile ...
```

{% hint style="info" %}
Under UNIX, the file must be user-readable only (i.e. permissions `0600` or `-rw-------`).&#x20;
{% endhint %}

{% hint style="danger" %}
Under Windows, there's no reliable way to enforce this, so use this method at your own risk!
{% endhint %}

It can contain as many profiles as you like, for usage for different "instances" of snapkup. The profile is the part of each row up until the first `:` and the password is the rest of the row. Rows that start with `#` or are empty are treated as comments.

**From prompt**

If the password is not provided with the methods above, it will be prompted for, unless the `--no-pwd-prompt` flag is specified. For batch operations, consider to always specify this flag.

### Initialize the backup directory

You need to initialize a directory to store the backups to. It's specified with the `--backup-dir` (or `-d`) flag, and this flag will need to be repeated for every command.

```
snapkup -d /home/my/MySnapkupDir init
```

It requires an empty directory and creates a shallow dir structure to organize the files, along with a `snapkup.dat` file (encrypted) that will store all the metadata. Also, generates the encryption and checksum keys.

### Register the directory(es) to back up as a root

Now we need to register one or more directories or files to actually backup. The command is:

```
snapkup -d /home/my/MySnapkupDir root add /home/my/MyImportantDir
```

All its contents will be recursively scanned when performing a snapshot (see below).

{% hint style="info" %}
The absolute path will be stored, to avoid ambiguities.
{% endhint %}

As many roots as you want can be stored; `root list` and `root del` commands are available to manage the list of roots.

### Take your first snapshot

As simple as:

```
snapkup -d /home/my/MySnapkupDir snap do -l "My first snapshot"
```
