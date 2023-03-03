# Help (no internet? no problem!)

Of _Stackoverflow_, _ChatGPT_ and all those helpful internet tutorials are always there for you, if you find yourself desperate in need for help. Yet, there are also ways on the CLI to directly get more information.

- [Help (no internet? no problem!)](#help-no-internet-no-problem)
  - [Manpages (Basic)](#manpages-basic)
  - [Command Help (Basic)](#command-help-basic)
  - [Shell History (Basic)](#shell-history-basic)
    - [Searching via reverse-i-search](#searching-via-reverse-i-search)
  - [Cheat (Advanced)](#cheat-advanced)

## Manpages (Basic)

Commands that are being installed via the software manager from your distribution normally come with so called _manpages_ (manual pages). Those manpages have detailed information and often also example how to use a programm. 

Manpages can be shown by typing:
```shell
man <command>

# eg. the ls command
man ls
```

You can also search for commands if you are unsure. For example search for related network manpages:
```shell
man -k network
```

Sometimes there are multiple manpages for the same term, but in different categories. If you executed the `man -k network` command, you will have noticed the numbers behind the manpage entries, which are related to categories. Categories can be:

1. User commands
2. System calls
3. C library functions
4. Devices and special files
5. File formats and conventions
6. Games and screensavers
7. Miscellanea
8. System administration tools and daemons

If there would be multiple entries for a manpage, type:
```shell
man <categorie number> manpage
man 8 ping
```

Of course there is manpage for man itself:
```shell
man man
```

## Command Help (Basic)

Most commands support either `<command> --help` or `<command> -h` flags to directly get the supported options and combinations.

For example type:
```shell
ls --help
# or
chmod --help
```

## Shell History (Basic)

You entered a command now on the x-th time and still cannot remember it and have to use it again.

Most shells support the `history` command. Depending on the setting of the `$HISTSIZE` variable you will see all the command line interactions from your previos commands.

The `$HISTSIZE` variable can be changed in your shell rc file. For example add to your `~/.bashrc` the following line:
```shell
export HISTSIZE=10000 # the last 10000 commands are being stored in your shells history file. eg. ~/.bash_history
```

You still need to activate changes in your shell rc. For bash that would be:
```shell
source ~/.bashrc
```

### Searching via reverse-i-search

You can also search directly by typing a string with `STRG+R` in your shell. This _reverse-i-search_ function should be enabled by default. If not, you can enable it. For example add the following to your `~/.bashrc`
```shell
# Enable reverse-i-search
"\e[A": history-search-backward
"\e[B": history-search-forward
```
You still need to activate changes in your shell rc. For bash that would be:
```shell
source ~/.bashrc
```

## Cheat (Advanced)

Cheat is a CLI tool that lets you build your own cheatsheets for topics or commands, which can be helpful, since your shell history or manpages will not always save you. Also it can be quicker than using _Stackoverflow_ for example.

[Github Link](https://github.com/cheat/cheat)