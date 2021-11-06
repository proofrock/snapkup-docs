# ❓ What is snapkup?

Snapkup is a simple backup tool that takes snapshots of your filesystem (or the parts that you'll decide), storing them efficiently and conveniently.

I wrote it because I wanted a single point to backup all the files in my linux system, and synchronize them to a cloud sync server. I wanted it to be incremental, of course, and to provide full deduplication; to compress the files and to encrypt them for privacy, as I also keep a copy of the backup on an USB disk.

I like its features. Please let me know if you'd like something else!

### Basic workflow

The basic flow to accomplish this can be summed up as:

* You initialize an empty directory that will store the backups;
* You register one or more backup roots: these are directory or files that will be snapshotted;
* You take one (and then more) snapshots. Snapkup lists all the filesystem tree for those roots, taking a copy of the contents;
* You can later restore the situation of the roots at any given snapshot;
* Of course, it's possible to list roots and snapshots and delete any of them, and perform all the other admin ops.

### Design choices

* Built with Go(lang). You get one statically linked binary, and that's all you need;
* Files are deduplicated: only one copy of a file is stored, across the filesystem and all the snapshots;
* Everything stored on-disk is encrypted, using `XChaCha20Poly1305;`
* Checksums, using authenticated 128-bit `SipHash`, are used to perform deduplication and integrity;
* By default, everything is compressed using `zstd -19;`
  * Incompressible files are stored as not compressed;
* Small files can be merged in "agglos", to reduce the number of files and make it more sync-friendly (e.g. for Dropbox);
* Snapkup favors features and code readability over speed. It's not slow, though!
* All paths are converted to absolute paths, for consistency;
* Cross-platform portability of backup archives is not a priority, though it should reasonably work.

### Future plans

* Ability to produce all outputs as JSON (maybe), for better script-ability;
* Ability to retrieve files from external filesystems, via SSH;
* Ability to back up data that come from the execution of a command (e.g. `crontab -l`);
* FUSE-mount a snapshot.
