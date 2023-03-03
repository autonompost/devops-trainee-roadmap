# More Basic Commands

- [More Basic Commands](#more-basic-commands)
  - [Search for files](#search-for-files)
    - [find (find files or directories)](#find-find-files-or-directories)
    - [locate (find files or directories)](#locate-find-files-or-directories)
  - [Interaction with files](#interaction-with-files)
    - [cat / less (show content of files)](#cat--less-show-content-of-files)
    - [grep / (z|x)grep (search for content in files)](#grep--zxgrep-search-for-content-in-files)
    - [Other important tools (it never ends)](#other-important-tools-it-never-ends)

## Search for files

Searching for files is one of the essential things you need to know, whether if you working directly on the CLI or writing shell scripts. The most common command is `find`, but there other even more powerful tools like [fzf - Fuzzy Find](https://github.com/junegunn/fzf).

### find (find files or directories)

The `find` command has a lot of flags but this section will just show a couple of them.

> if you have installed [cheat](./help.md#cheat) you will even see more examples

Try the following examples:
```shell
find ~/ -type d # will find all directories in your $HOME 
find ~/ -type f # will find all files in your $HOME 
find . -type f -name "*.sh" # will find all files with an .sh extension in the current directory you are in
find /etc -type f -ls # will find all files in the /etc directory and display file information
find /etc -type f -exec ls -la {} \; # the same command but with -exec flag
```
As you can see `find` also is capable of actually executing commands on the found files. Later when we talked about [Pipes](./shell_basics.md#pipes) you will see that there are again more ways to do things.

### locate (find files or directories)

There is another useful command `locate` which builds its own database file and therefore is able to search must faster than `find`.

In order to use `locate` the `mlocate` package needs to be installed. Depending on your distribution, see also [Package Management](./package_management.md) the package manager and installation differs.

Before you can use `locate` the file DB needs to build. To do that you will need `sudo` permissions, see also [the sudo section of users and groups](./users_and_groups.md#sudo-execute-commands-with-elevated-rights) For that type the following:
```shell
sudo updatedb
```
After that you will be able to search for files system-wide. For example:
```shell
locate myfile
locate passwd
```

## Interaction with files

The following commands are literary on the tip of the iceberg when it comes to working with files in Linux.

### cat / less (show content of files)

The following tools can be used to view files, when it comes to `less` also to search in files directly. `cat` and `less` can also be used as so-called `PAGER`, see also [Shell Environment Variables](./shell_basics.md#environment-variables-basic).

First create a file with the following command:
```shell
cat << EOF > ~/mypoem
In a world of proprietary code,
Where access is limited and control bestowed,
There's a movement rising up,
A force for good that won't let up.

Free software, open source,
A community that charts a new course,
Where knowledge is shared and code is free,
A world where collaboration is key.

The power of code in the hands of the few,
Can create a world that's unfair and askew,
But open source levels the playing field,
A world of possibility it does yield.

From the smallest script to the grandest app,
Open source is where innovation takes its nap,
Where ideas can flourish and grow,
A world where creativity can freely flow.

So let us celebrate this movement bold,
That seeks to make our future bright and bold,
Free software and open source,
A revolution that we can all endorse.
EOF
```

Now we use `less` and `cat` to look at the file:
```shell
cat ~/mypoem # output the complete content of mypoem to the shell
less ~/mypoem # open the file up with the less command
```

When the file is opened up with `less` you can use the following basic commands inside:
```shell
Use the arrow keys to scroll up and down.
Press the space bar to move down one page at a time.
Press the b key to move up one page at a time.
To search for a specific term, press the / key and type in the term you want to search for. Press Enter. Use the n key to move to the next occurrence of the term.
To exit the less command, press the q key.
```

### grep / (z|x)grep (search for content in files)

With the different version of the `grep` it is possible to search for strings in files. If you have ascii files that are compressed, there are also grep version like `zgrep` for gzipped or `xgrep` for xv compressed files.

Try the following:
```shell
grep open ~/mypoem # grep for all lines containing the word open case sensitive
grep -i Open ~/mypoem # grep for all lines containing the word open case insensitive
grep -vi open ~/mypoem # grep for all lines except those containing the word open case insensitive
grep -Ei "^open" ~/mypoem # grep for all lines that begin with the word open case insensitive
grep -REi "^open" ~/* # grep recursive in all files in the $HOME directory that match lines that begin with the word open case insensitive
```

Those `flags` also work on other versions of the `grep` command.

### Other important tools (it never ends)

In Linux you have a lot of tools at hand to work with files. Take a basic look at the following commands and remember what they are about.

- cut
- tail
- head
- tr
- sort

and so on ..

