Tools like cyphertite are great.

Sometimes they need a wrapper script to make them even better.

Since it helps to explain with a real world example, lets say you have a
media subdirectory with tons of data archived via cyphertite.

Lets say you lost your disk.

Lets say you are not online 24/7 and you reboot frequently to test os
kernels.

You don't have time to extract the whole archive in one go, so how can
you make progress by extracting a few files at a time?

I have filed an issue[1] with cyphertite to do the equivalent
internally, but until that is working, there is the following
'ctfastextract' script which:

1) loads the list of files (and types) into memory
2) utilizes an exclusion regex '-e <regex>' to ignore paths
3) utilizes an inclusion regex '-i <regex>' to ignore all but the inclusion paths (does nothing if not specified)
4) orders paths as dirs, files, symlinks, hardlinks
5) extracts up to 30 paths in one go
6) utilizes a total path limit '-l <count>' if a person wishes to stop
   before completely extracting everything

For example:

  ctfastextract -e xvpics -l 50 my.media

This will extract 'my.media' excluding paths that match 'xvpics' and stop
after 50 paths have been extracted.

Please note, at this time, the ctfastextract only counts a path if the local
filesystem does not have a given path already.  It skips downloading a file
if it already exists.

Future enhancements include:

1) using the size of the file in the filesystem vs metadata to determine if an
   extraction is needed for a locally truncated file or somesuch
2) using the hash of the file in the filesystem vs metadata to determine if an
   extraction is needed (can cyphertite provide this via -tvf?)

If you have other ideas or improvements, please send me diffs or pull
requests or whatever.

Thanks!

[1] https://github.com/conformal/cyphertite/issues/58
-- 
Todd Fries .. todd@fries.net

 ____________________________________________
|                                            \  1.636.410.0632 (voice)
| Free Daemon Consulting, LLC                \  1.405.227.9094 (voice)
| http://FreeDaemonConsulting.com            \  1.866.792.3418 (FAX)
| PO Box 16169, Oklahoma City, OK 73113-2169 \  sip:freedaemon@ekiga.net
| "..in support of free software solutions." \  sip:4052279094@ekiga.net
 \\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\
                                                 
              37E7 D3EB 74D0 8D66 A68D  B866 0326 204E 3F42 004A
                        http://todd.fries.net/pgp.txt
