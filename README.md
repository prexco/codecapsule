# CodeCapsule
=============

CodeCapsule - Manage multiple repositories as a single project
(Very similar to [repo] that is used to manage the Android open source project.)
This one is lighter and only requires Bash, which is usually available with any installation of git.

This is essentially a bootstrapper for [codecapsule-util], which is automatically installed within an initialised directory.

equirements
------------

* git
* bash (version 3 or newer)

Installation
------------

Simply download `codecapsule` and put it in your path.

   # Step 1:  Download with curl ...
   curl https://raw.githubusercontent.com/prexco/codecapsule/master/codecapsule -o codecapsule
   # or wget.
   wget https://raw.githubusercontent.com/prexco/codecapsule/master/codecapsule

   # Step 2:  Make the file executable.
   chmod 755 codecapsule

   # Step 3:  Move codecapsule somewhere to be in your path.
   # This is for a system-wide installation:
   sudo mv codecapsule /usr/local/bin

   # If you don't have sudo/root access, or if you don't want to make it available system-wide,
   # alternatively could be to put executables in ~/bin and make sure it
   # is in your path.
   mv codecapsule ~/bin

Command Reference
-----------------

The `help` and `init` commands can be used from anywhere.  
All other commands can be executed from anywhere within an initialised directory, including inside any subdirectory.

### codecapsule help

Shows a help message. When used in an initialised directory, the help message will list all the available commands.

Examples:

   codecapsule help


### codecapsule init REMOTE [DEST]

Initialises the current directory.  
`REMOTE` is the URL to a git repository that has a [capsule_file]. Downloads the [capsule_file] and [codecapsule-util] into a `.codecapsule/` directory.

* REMOTE - This is the git repository URL. It's the same as what you'd use for "git clone".
* DEST - Destination for the codecapsule-initialised directory.

Once a directory is initialised, additional commands show up in `codecapsule help`.

Examples:

   # Sets up a codecapsule directory in ./capsule_file
   cd ~
   codecapsule init http://github.com/example/capsule_file.git
   cd capsule_file
   codecapsule sync

   # Specify a directory
   cd ~
   codecapsule init http://github.com/example/another.git the-destination
   cd the-destination
   codecapsule sync

### gg status

Shows the status of your repositories.  If a repository is clean, this only shows a short message.  If it is dirty it shows the entire `git status` message.

Examples:

   gg status

Result:

   [codecapsule] .codecapsule/gg-core: clean
   [codecapsule] .codecapsule/manifest: clean
   [codecapsule] projects/project-star: dirty
   On branch codecapsule
   Your branch is up-to-date with 'origin/codecapsule'.
   Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

      modified:   file1
      modified:   client.cpp
      modified:   engine.cpp

   no changes added to commit (use "git add" and/or "git commit -a")
   [codecapsule] dir1: clean
   [codecapsule] prexco/project: clean
   [codecapsule] prexco/configs: clean

### codecapsule sync

Synchronises the [capsule_file], [codecapsule-util] and every repository listed in the capsule_file.  
First it executes a `git fetch` to pull in the remote's history.  
After that, it attempts a rebase. If the rebase fails, it falls back to a pull and push with possible merge conflicts detected and then they would need to be handled manually.

Can be executed anywhere inside an initialised directory.

Examples:

   codecapsule sync


[codecapsule-util]: https://github.com/prexco/codecapsule-util
[repo]: https://source.android.com/source/using-repo.html
