## Packages ##
> Installing from source can get messy, if you compile rather do:

    // Build dependencies (If available in repost but you want newer version)
    apt-get build-dep someapp
    // If there is no configure first run autogen.sh
    ./configure
    ./make 
    // Now instead of "make install" use checkinstall, this will keep track.
    sudo checkinstall
    // Now you can remove a package by doing 
    sudo dpkg -r someapp

## DPKG
> Interesting and helpful functions for packages.

## APT
`sudo add-apt-repository <repo>` Add repository.

* `dpkg -s <packagename>` See what version a package is and get info about that package.
* `apt-cache showpkg inkscape | grep "gtk"` Check application dependency and other information regarding app. The grep command simply searches for something inside the results.

## System
* `sudo lsof -i -P` What TCP/IP ports are open.
* `blkid` Find HDD device id.
* `/etc/fstab` And create automount mount by editing.
* `finger {userid}` Find out what someone is up to.
* `df` Checking for disk space on available volumes.
* `alias {name} '{command}'` Put the command in 'single quotes'. More useful in your .cshrc file.

## General Files & Folders
* `chmod +x filename` Make a file executable.
* `ln -s /home/myname/sh/runme.sh /usr/local/bin/runme` Create symlink.
* `rmdir {dirname}` Only works if `{dirname}` is empty.
* `rm -r {dirname}` Remove all files and subdirs. Careful!
* `pwd` Shows your current full path.
* `du -h --max-depth=1` Check for size of folders in current working directory.
* `find {filespec}` Works with wildcards. Handy for snooping.
* `find {filespec} > {filename}` Redirect find list to file. Can be big!
* `find . -name "*.bak" -type f -delete` Find specific file types and delete them.
* `find . -name "*.bak" -type f` Test files found with this command before running eg. -delete

## Copy a file or directory
* `cp {file1} {file2}`  
* `cp -r {dir1} {dir2}` Recursive, copy directory and all subdirs.
* `cat {newfile} >> {oldfile}` Append newfile to end of oldfile.
## Move (or rename) a file
* `mv {oldfile} {newfile}`  Moving a file and renaming it are the same thing.
* `mv {oldname} {newname}`
* `rsync -r dir1/ dir2` Syncs a directory with another, `/` means content of.
* `rsync -a` syncs recursively and preserves all files.
* `rsync -azP username@remote_host:/home/username/dir1 place_to_sync_on_local_machine` z = compression, P = progress

## Help on any Unix command
* `man {command}`   Type man ls to read the manual for the ls command.
* `whatis {command}`  Give short description of command. (Not on RAIN?)
* `apropos {keyword}`   Search for all Unix commands that match keyword, eg apropos file. (Not on RAIN?)

## List a directory
* `ls {path}` It's ok to combine attributes, eg ls -laF gets a long listing of all files with types.
* `ls {path_1} {path_2}` List both {path_1} and {path_2}.
* `ls -l {path}` Long listing, with date, size and permissions.
* `ls -a {path}` Show all files, including important .dot files that don't otherwise show.
* `ls -F {path}` Show type of each file. "/" = directory, "*" = executable.
* `ls -R {path}` Recursive listing, with all subdirs.
* `ls {path} > {filename}` Redirect directory to a file.
* `ls {path} | more`  Show listing one screen at a time.

## Text files
* `more {filename}` View file one screen at a time.
* `less {filename}` Like more, with extra features.
* `cat {filename}` View file, but it scrolls.
* `cat {filename} | more` View file one screen at a time.
* `page {filename}` Very handy with ncftp.
* `pico {filename}` Use text editor and don't save.
* `touch {filename}` Create file.
* `diff {file1} {file2}` Show the differences.
* `sdiff {file1} {file2}` Show files side by side.
* `grep '{pattern}' {file}` Find regular expression in file.
* `sort {file1} > {file2}` Sort file1 and save as file2.
* `sort -o {file} {file}` Replace file with sorted version.
* `spell {file}` Display misspelled words.
* `wc {file}` Count words in file.

## Pipes and Redirection
* `{command} > {file}` Redirect output to a file, eg ls > list.txt writes directory to file.
* `{command} >> {file}` Append output to an existing file, eg cat update >> archive adds update to end of archive.
* `{command} < {file}` Get input from a file, eg sort < file.txt
* `{command} < {file1} > {file2}` Get input from file1, and write to file2, eg sort < old.txt > new.txt sorts old.txt and saves as new.txt.
* `{command} | {command}` Pipe one command to another, eg ls | more gets directory and sends it to more to show it one page at a time.

## Permissions
> You can change file permissions with letters:

    u = user (yourself)     g = group   a = everyone
    r = read    w = write   x = execute

    chmod u+rw {filespec}   Give yourself read and write permission
    chmod u+x {filespec}    Give yourself execute permission.
    chmod a+rw {filespec}   Give read and write permission to everyone.

> Change file ownership (user:group):
> Add -R to do a directory recursively.

    chown himanshu:friends tmpfile
