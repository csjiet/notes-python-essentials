
# 1. `tar` ("`T`ape `AR`chive format")

> "Tape Archive" or "tar" originates from magnetic tape drives that were used for data storage and backup/ archival of files and directories onto magnetic tapes. Information is packed single stream of data that could be easily written to tape and later read back.

- Use: **Bundle files** together into a **single archive** (instead of a messy tree directory structure).
	- NOTE: Tar files do not provide compression on their own
- Extension: `.tar` only.

# 2. `tar` + `.compression`
- Use: Bundle files together (`.tar`) + compression algorithms ({list below}):
- Common compression algorithms:
	- `.tar.gz/ .tgz`: 
		- tar archive + gzip compression (Files are first bundled together using tar, and then the entire archive is compressed with the gzip algorithm.)
	- `.tar.bz2`:
		- tar archive + bzip2 compression (Files are bundled together using tar and then compressed with bzip2 algorithm.)
	- `.tar.xz`:
		- tar archive + xz compression (Files are bundled together using tar and then compressed with xz algorithm.)

## Compressed file extraction commands
### Extracting`.tar.gz`:
``` bash
tar -xzvf yourfile.tar.gz
```
- `-x`: Extract files.
- `-z`: Use gzip to uncompress the file.
- `-v`: Verbose mode (optional, provides detailed output).
- `-f`: Specifies the archive file to operate on.

### Extracting`.tar.bz2`:
### Extracting`.tar.xz`:
