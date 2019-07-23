---
description: A few examples of backing up data to $ARCHIVE
---

# Syncing with $ARCHIVE

## $CENTER1 &lt;-&gt; $ARCHIVE

The volatile, high performance scratch filesystem, $CENTER1, is not intended for permanent storage. Users are responsible for backing up any critical data either to their own storage, or to $ARCHIVE. The two methods recommended to backup  files are either `sftp`, `scp`, or `rsync` via `ssh`. Here are examples of using these commands.

{% hint style="info" %}
To simplify these processes, set up SSH keys for easier authentication onto bigdipper.alaska.edu first.
{% endhint %}

### sftp a file

```
Login to a chinook login node.
$ cd $CENTER1/local-subdir
$ sftp bigdipper.alaska.edu
> cd /archive/PROJECT/username/remote-subdir
> put file1
> quit
```

### scp a sub-directory

```text
Login to a chinook login node.
$ scp -rp $CENTER1/local-subdir \
bigdipper.alaska.edu:/archive/PROJECT/$USER/remote-subdir
```

### rsync via ssh

```text
Login to a chinook login node.
$ rsync -av --rsh=ssh $CENTER1/local-subdir/ \
bigdipper.alsaka.edu:/archive/PROJECT/$USER/remote-subdir/
```

{% hint style="info" %}
Note the trailing "/" in the path names. They are important. For more information, see the [rsync man page](https://linux.die.net/man/1/rsync).
{% endhint %}

All of these transfers can be automated and executed as a batch job in the chinook transfer queue, or as a cron job on a chinook login node.

