---
description: How to best return data back from tape in the $ARCHIVE file system
---

# Staging data from tape in $ARCHIVE

$ARCHIVE is a special kind of file system that uses hierarchical storage management (HSM) to allow for higher utilization of storage than the physical spinning disk capacity would normally allow. This is done by copying data to tapes in a magnetic tape library for long term storage, but in so doing, the process erases the file off of the disk capacity. In order to access your file again, it must first be "staged" back from tape, or copied from tape to disk for processes to make use of it. Processes can be anything from scripts, development environments / editors, and data manipulation tools like `rsync` or `cp`.

{% hint style="info" %}
The act of moving a file or directory (mv) within the $ARCHIVE file system is an immediate operation and does not require staging the data back from tape.
{% endhint %}

## Confirm a file is offline in the $ARCHIVE file system

The first thing you should verify before attempting to access your files or directories via any method while on $ARCHIVE is that the file is actively "online", meaning that it resides on hard disk capacity and not "offline" or solely on tape. To verify this, run the following command on your file:

```
$ sls -D <path_to_file>
```

For example, if the file is in the present working directory, you would run the following for a file called test.txt:

```
$ sls -D test.txt
```

The output from that command will look something like this:

```
/versity/archive/EXAMPLE/user/test.txt:
  mode: -rwxr-s---  links:   1  owner: user  group: example   
  length: 10774625242  inode:   823419671.1
  offline;
  copy 2: ------ Oct  6  2019    25d246a.392078b m2 601256
  copy 3: ------ Oct  6  2019    25d246a.392078b m2 601257
  access:        Oct  6  2019  modification: Oct  6  2019
  changed:       Oct  6  2019  attributes:   Oct  6  2019
  creation:      Sep  30 2019  residence:    Oct  8  2019
```

You can see in the output above, a lot of metadata about your file is returned, but the most important section for this document is the line stating "offline". That indicates that the file needs to be staged back from tape. If the text "offline" does not appear, it is currently on disk and you do not need to continue on with this document.

## Batch Stage Files

To bring back one or more files from tape is best done by using the homegrown command `batch_stage`. This command looks at the file(s) requested and orders them to be most efficiently returned from tape. If no files need to be staged back from tape, nothing will happen and the command will return immediately.

{% hint style="info" %}
Always use batch_stage to return files back from tape to prevent very slow load times from tape!
{% endhint %}

Below are examples of using batch_stage:

1. Stage all files in a directory using absolute paths
     ```
     $ batch_stage $ARCHIVE/data/*`
     ```

2. Stage all files in a directory recursively using absolute paths
     ```
     $ find $ARCHIVE/data -type f | batch_stage -i
     ```

3. Stage all files in a directory using relative paths (Option 1)

     ```
     $ cd $ARCHIVE/data
     $ batch_stage *
     ```

4. Stage all files in a directory using relative paths (Option 2)

     ```
     $ cd $ARCHIVE/data
     $ ls -1 | batch_stage -i
     ```

5. Stage all files in a directory recursively using relative paths
     ```
     $ cd $ARCHIVE/data
     $ find . -type f | batch_stage -i
     ```

6. Stage all files in a directory recursively using relative paths
     ```
     $ batch_stage -r $ARCHIVE/data
     ```
