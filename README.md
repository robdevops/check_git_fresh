# check_git_fresh
Warns if a local git repo is behind or ahead of the remote. Can optionally check if local files are also recent.

## Usage
```
Usage: check_git_fresh -r <REPO PATH> [ -f <FILE PREFIX> ] [ -a <FILE AGE SECONDS> ] [ -s <FILE SIZE IN BYTES> ]

-r <REPO PATH> (Required). This is the path you cloned the repo into, and it contains the subdirectory .git/.
-f <FILE PREFIX> (Optional). Only look for changes to files matching this prefix. If unspecified, '*' will be used.
-a <FILE AGE IN SECONDS> (Optional). Mimick the nagios check_file_age plugin, giving a warning if the newest file is older than SECONDS. 
-s <FILE SIZE IN BYTES> (Optional). Mimick the nagios check_file_age plugin, giving a warning if the newest file is below BYTES.
```

## Example execution
`check_git_fresh -r /home/rob/check_git_fresh`

`check_git_fresh -r /home/rob/check_git_fresh -f check`

`check_git_fresh -r /home/rob/check_git_fresh -f check -a 400 -s 2500`


## Example warning output

### Untracked change, or tracked but not committed
`Warning: 1 uncommitted change`

### Change committed but not pushed
`Warning: 1 unpushed commit`

### Remote ahead
`Warning: Your branch is behind 'origin/master' by 3 commits, and can be fast-forwarded.`

### File stale
`Warning: Files matching check* are at least 500 seconds old.`

### File truncated
`Warning: /home/rob/check_git_fresh/check_git_fresh is only 123 bytes.`

## Example OK output
`OK: latest file /home/rob/check_git_fresh/check_git_fresh is 200 seconds old and 2539 bytes`
