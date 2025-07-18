# Available RCS Storage 

## High Performance Computing Storage

High Performance Computing storage \($CENTER1\) is fast, high throughput, scratch storage available to Chinook users. $CENTER1 is a Lustre filesystem best used for large files. Reading or writing many small files may result in a noticeable performance reduction. As a scratch workspace, data in $CENTER1 is not backed up. Files that need long-term storage should be copied to a different system or filesystem, such as $ARCHIVE.

Projects are subject to a quota in $CENTER1. Quotas may be checked using the “show\_storage” command. Always check to see if there is storage available for your file to be written as files written that go over the quota may be truncated, unwritten, or block move and write access to the filesystem.

Subsidized quota: 1 TB

## Online Spinning Disk

Online spinning disk is used to share data and storage to RCS managed VMs. Data may be backed up automatically to $ARCHIVE for an additional service fee or Principal Investigators may back up online spinning disk data manually to their $ARCHIVE account using their subsidized 30 TB or any additional purchased $ARCHIVE storage. Online spinning disk storage will generally perform slower when used with high performance computing.

## Offline Tape Archive

The offline tape archive \($ARCHIVE\) is a long-term storage solution for infrequently accessed data, such as retention of completed work or an archive of data. Data stored in $ARCHIVE is written out to magnetic tape and must be retrieved when copied to another filesystem, resulting in very slow access times. Files in $ARCHIVE should be copied or moved to another filesystem before modifying or using the files.

Principal Investigators in $ARCHIVE are subject to quota. When quota is reached files may no longer be written, and a file that is currently being written to the filesystem may be truncated or deleted, and access to writing and moving files may be lost. It is always recommended to check that there is enough space to write your file. Quotas and current usage can be viewed with the “show\_storage” command.

Subsidized quota: 30 TB
