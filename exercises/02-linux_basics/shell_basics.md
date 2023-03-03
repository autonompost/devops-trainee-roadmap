# Shell Basics

- [Shell Basics](#shell-basics)
  - [Environment Variables (Basic)](#environment-variables-basic)
  - [Shell RC File (Basic)](#shell-rc-file-basic)
    - [Shell Aliases (Advanced)](#shell-aliases-advanced)
    - [Shell Functions (Advanced)](#shell-functions-advanced)
  - [Shell Profile (Basic)](#shell-profile-basic)
  - [Other Important Things to know](#other-important-things-to-know)
    - [Exit Codes](#exit-codes)
    - [Pipes](#pipes)
    - [Output Redirection](#output-redirection)


## Environment Variables (Basic)

Linux shell environment variables are system variables that are used by the shell and other command-line utilities to configure various aspects of their behavior. These variables are set by the shell or by the system itself, and can be accessed and modified using shell commands.

Environment variables can be used to customize the behavior of the shell and other command-line utilities, as well as to provide information to applications and scripts. For example, the HOME environment variable specifies the path to the user's home directory, which can be used by various applications to store user-specific data.

Some environment variables are set by default by the system or shell, while others may need to be set manually by the user. The values of environment variables can be viewed and modified using shell commands such as echo and export.

You can type `env` in your shell to see what enviroment variables are configured.

The most important and common environment variables are:

| Variable | Description |
| --- | --- |
| PATH | Contains a colon-separated list of directories in which the shell looks for executable files. |
| HOME | Contains the path to the user's home directory. |
| USER | Contains the name of the current user. |
| PS1 | Defines the primary prompt string for the shell. |
| TERM | Contains the type of terminal being used. |
| LANG | Specifies the language and locale settings for the current user. |
| SHELL | Contains the path to the current shell executable. |
| PWD | Contains the path to the current working directory. |
| EDITOR | Specifies the default text editor to use. |

## Shell RC File (Basic)

Each Linux Shell has possibities to configure or add additional functionality to the shell environment. The RC file is read for each non-login and login shell.

Configuration are being added to so called `RC (run command)` files.

Examples:
```shell
~/.bashrc # Bash Shell RC files
~/.zshrc # ZSH Shell RC file
~/.kshrc # KSH Shell RC file
```

### Shell Aliases (Advanced)

Shell aliases are shortcuts you can define to make accessing complex commands easier.

Type and display the current configured `alias` command list on your system.

To configure an `alias` you have to make an entry to your shell's RC file.

For example for `~/.bashrc`:

```shell
nano ~/.bashrc # open you .bashrc file for editing
# go to the bottom of the file and add the following line
alias cdl='cd /var/log'
```

To activate changes in your shell RC file you have to either start a new shell or load the RC file again in your running session.

For example:

```shell
source ~/.bashrc # read and activate your current state of your .bashrc including your alias entry
```

Now the alias should be available on the CLI.

Type `cdl` and you should be automatically be in the path `/var/log`.

Type `alias` or `alias | grep cdl` and you should see your entry now also activated.

### Shell Functions (Advanced)

It also possible to create shell functions inside the RC file. This gives you all all the scripting possibilities of your shell.

Later in the Bash Scripting exercises you will also learn to use functions. 

Here just a simple bash function example:

```shell
function git-acp() {
    # check if Git is installed
    if ! command -v git &> /dev/null; then
        echo "Error: Git is not installed." >&2
        return 1
    fi
    
    # check if there are any changes to commit
    if git status --porcelain | grep -q '^M'; then
        # check if a commit message was provided as a parameter
        if [ $# -eq 0 ]; then
            # if no commit message was provided, use a default message
            commit_msg="Auto-commit by git-acp"
        else
            # if a commit message was provided, use it
            commit_msg="$1"
        fi
        
        # add all changes to the Git staging area
        git add .
        
        # commit the changes with the provided commit message
        git commit -m "$commit_msg"
        
        # push the changes to the default upstream branch
        git push
    else
        echo "No changes to commit."
    fi
}
```

The function `git-acp` can now be called in your shell with:

```shell
git-acp "My commit message"
```

## Shell Profile (Basic)

In the section about [Shell RC File](#shell-profile-basic) a file RC was created which is being used for non-login and login shells.

The Shell Profile file is being soley being used for login shells.

It has the same functionality as the RC file.

For example:

```shell
~/.bash_profile # the profile for the Bash Shell
~/.zshrc_profile # the profile for the ZSH Shell
```

## Other Important Things to know

### Exit Codes

### Pipes

### Output Redirection


