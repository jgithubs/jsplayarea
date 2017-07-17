# Software, GitHub for documentation and source code

* [Hardware Project](hw-project.md)

## Links
* Tortois Git, https://tortoisegit.org/
* Git for Windows, https://git-for-windows.github.io/

## GitBash Commands

The example below uses GitBash that comes with the Git for Windows installation.
The GitBash runs on Windows and has a command window that is similar to linux.
The commands below are in the GitBash command shell.

Download source tree
```
gitbash> git clone https://github.com/jgithubs/jsplayarea
gitbash> cd jsplayarea
```

Add/remove files to directory
```
gitbash> git add <filename>
gitbash> git rm <filename>
gitbash> git mv <name1> <name2>
```

Add/remove directory
```
gitbash> git rm -r --cached <dirname>
```

Status of git files.
A series of files that has been modified.
These files are "not staged" and need to be added to the commit area.
```
gitbash> git status
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#       modified:   README.md
#       modified:   hw-audio-hdmi.md
#       modified:   hw-mount-usb.md
#       modified:   hw-project.md
#       modified:   sc-print3d.md
#       modified:   sc-project.md
#       modified:   sw-audio-alsa.md
#       modified:   sw-development.md
#       modified:   sw-github.md
#
no changes added to commit (use "git add" and/or "git commit -a")
```

Use the "add" command to stage (or add) files to commit area.
You can use individual filenames or wild cards.
```
gitbash> git add README.md
warning: CRLF will be replaced by LF in README.md.
The file will have its original line endings in your working directory.

gitbash> git add hw-*
warning: CRLF will be replaced by LF in hw-mount-usb.md.
The file will have its original line endings in your working directory.
```

After adding all of the remaining files, get the status.
These files are now ready to be "committed".
```
gitbash> git status
warning: CRLF will be replaced by LF in README.md.
The file will have its original line endings in your working directory.
warning: CRLF will be replaced by LF in hw-mount-usb.md.
The file will have its original line endings in your working directory.
warning: CRLF will be replaced by LF in sc-project.md.
The file will have its original line endings in your working directory.
warning: CRLF will be replaced by LF in sw-audio-alsa.md.
The file will have its original line endings in your working directory.
warning: CRLF will be replaced by LF in sw-development.md.
The file will have its original line endings in your working directory.
warning: CRLF will be replaced by LF in sc-project.md.
The file will have its original line endings in your working directory.
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#       modified:   README.md
#       modified:   hw-audio-hdmi.md
#       modified:   hw-mount-usb.md
#       modified:   hw-project.md
#       modified:   sc-print3d.md
#       modified:   sc-project.md
#       modified:   sw-audio-alsa.md
#       modified:   sw-development.md
#       modified:   sw-github.md
#
```

Add a comment before with the commit command.
A series of warning about line feeds are fine.
```
gitbash> git commit -m "Added more updates"
[master warning: CRLF will be replaced by LF in README.md.
The file will have its original line endings in your working directory.
warning: CRLF will be replaced by LF in hw-mount-usb.md.
The file will have its original line endings in your working directory.
warning: CRLF will be replaced by LF in sc-project.md.
The file will have its original line endings in your working directory.
warning: CRLF will be replaced by LF in sw-audio-alsa.md.
The file will have its original line endings in your working directory.
warning: CRLF will be replaced by LF in sw-development.md.
The file will have its original line endings in your working directory.
warning: CRLF will be replaced by LF in sc-project.md.
The file will have its original line endings in your working directory.
b65dc00] Added more updates
warning: CRLF will be replaced by LF in README.md.
The file will have its original line endings in your working directory.
warning: CRLF will be replaced by LF in hw-mount-usb.md.
The file will have its original line endings in your working directory.
warning: CRLF will be replaced by LF in sc-project.md.
The file will have its original line endings in your working directory.
warning: CRLF will be replaced by LF in sw-audio-alsa.md.
The file will have its original line endings in your working directory.
warning: CRLF will be replaced by LF in sw-development.md.
The file will have its original line endings in your working directory.
 9 files changed, 200 insertions(+), 54 deletions(-)
```

A this point nothing has been put in GitHub.
The file changes are still local.
The committed file now needs to be pushed to GitHub that requires username and password.
```
gitbash> git push
Username:
Password:
Counting objects: 21, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (11/11), done.
Writing objects: 100% (11/11), 3.94 KiB, done.
Total 11 (delta 9), reused 0 (delta 0)
remote: Resolving deltas: 100% (9/9), completed with 9 local objects.
To https://github.com/jgithubs/jsplayarea
   4f9ee3a..b65dc00  master -> master
```

Go to the GitHub site and find your commit or query it from you host.
There may be hundred of commits, just print the last two.
You should see a comment with your username and your comment.
If your email is not correct, see the next section to personalize your environment.
```
gitbash> git log -2
commit b65dc00fff425370253d88a961339837ef1a0cc3
Author: username <youremail@gmail.com>
Date:   Sat Jul 15 23:50:23 2017 -0600

    Added more updates

commit 4f9ee3a55ac0cc1b43e641243357a332b98f4a03
Author: username <youremail@gmail.com>
Date:   Tue Jul 11 20:41:31 2017 -0600

    Add usb, rfid transfer changes
```

## Personalizing GitHub

If you commit changes with default git settings, GitHub tree will show strange users.
Take the time to add your proper git information.
```
gitbash> git config --list
gitbash> git config --global user.name "first last"
gitbash> git config --global user.email <email-address>
```

