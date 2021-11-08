# 📍 root del

## Syntax

{% hint style="warning" %}
Please be sure to read the [App-wide args](../../app-wide-args.md) page to understand the basics
{% endhint %}

```
snapkup -d somedir root del <root>
```

## Aliases

The short alias is `rm`, so the command can be shortened to `snapkup [...] r rm`

## Description

Deletes a [root ](./#description)from the list. The absolute path must be specified, as listed by [root list](root-list.md).

## Example

```
snapkup -d C:\MyBkpDir root del C:\MyDirToBackup

# Outputs:
# Root correctly deleted (C:\MyDirToBackup)
```
