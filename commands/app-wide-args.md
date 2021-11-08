# 📖 App-wide args

## Syntax

```
snapkup --backup-dir somedir [--profile myProfile] [--no-pwd-prompt] <commands>
```

## Aliases

`--backup-dir` --> `-d`

`--profile` --> `-p`

No aliases for `--no-pwd-prompt`

## Description

The general commandline arguments for snapkup, which are valid for all the commands, are used to:

* provide the backup directory to use for every command
* provide the password for the (mandatory) encryption

### Provide the backup directory

It's specified via `--backup-dir` or `-d`. The directory will be initialized with the `init` command, and used for all the other commands, which expect an already-initialized directory.

It must be specified for every invocation of snapkup.

### Provide the password&#x20;

There are three ways to do so: via an environment variable; via a credentials file in the filesystem; or via prompt in the application.

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
# This is a comment
myProfile:MyCoolPwd
myOtherProfile:AnotherPassword
```

Then start snapkup specifying the profile:

```
snapkup --profile myProfile ...
```

{% hint style="info" %}
Under UNIX, the file must be user-readable only (i.e. permissions `0600` or `-rw-------`).
{% endhint %}

{% hint style="danger" %}
Under Windows, there's no reliable way to enforce this, so use this method at your own risk!
{% endhint %}

It can contain as many profiles as you like, for usage for different "instances" of snapkup. The profile is the part of each row up until the first `:` and the password is the rest of the row. Rows that start with `#` or are empty are treated as comments.

**From prompt**

If the password is not provided with the methods above, it will be prompted for, unless the&#x20;

`--no-pwd-prompt`&#x20;

flag is specified. For batch operations, consider to always specify this flag.
