# notes-and-tricks
Reminders (for myself, mostly) about how to do various simple things that I do occasionally and always forget

## Transferring files

### Speeding up a single file transfer over ssh using multiple processes

Use lftp to get the file `/home/username/filename` using 6 parallel connections:

`lftp -e 'pget -n 6 sftp://username@server/home/username/filename'`

This seems useful, e.g., for high latency connections. I'm not sure exactly
why, but it speed things up transferring from a server in Seattle to a server
in Bristol, for example.

See also http://superuser.com/questions/75681/inverse-multiplexing-to-speed-up-file-transfer/305236.

### Speeding up rsync when it is cpu-limited by ssh

`rsync -e "ssh -c arcfour" [...]`

Maybe this is less secure than whatever the default ssh cipher is. See http://en.wikipedia.org/wiki/RC4.

## Video encoding

Convert a sequence of png images (named `0000000.png`, `0000001.png`, ...)
into a video with a bitrate of 1500k:

`avconv -i %07d.png -vcodec mpeg4 -b 1500k output.avi`

(can also replace `mpeg4` with `mjpeg`, `mpeg2video`,... something similar for webm.)
