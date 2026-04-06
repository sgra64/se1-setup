## 5. *Aliases* and *Functions*

Topics:
- a) [What is an *alias*?](#a-what-is-an-alias)
- b) [What is a *shell function()*?](#b-what-is-a-shell-function)


---
&nbsp;
### a) What is an *alias*?

*Aliases* are short-cuts for user-defined *Shell* commands that
simplify typing. *Aliases* are usually defined in
*.bashrc* / *.zshrc* files.

*Aliases* are not inherited to sub-processes and hence definitions
must be loaded every time a *Shell* process starts
(the reason is that *aliases* only make sense in *Shell* processes
and not in other processes and are therefore not automatically
inherited).

Examples *alias* definitions from a `.bashrc` file are:

```sh
alias vi="vim"              # use vim for vi, -u ~/.vimrc
alias l="ls -alFog"         # detailed list with dotfiles
alias ll="ls -l"            # detailed list with no dotfiles
alias grep="grep --color=auto"              # use colored output
alias path="echo \$PATH | tr ':' '\012'"    # show pretty PATH

# various aliases to shortcut git-commands
alias gt="git status"
alias log="git log --oneline"
alias br="git branch -avv"
alias gls="git show --name-status"
```


---
&nbsp;
### b) What is a *shell function()*?

*Aliases* allowed to substitute shortcuts, but not more than that.

*Functions* allow more comprehensive definitions of commands in
*Shell*-scripts that can be called from within scripts or from
the command line by function names.

Like *aliases*, *functions* only make sense for *Shell* processes
and are hence not inherited to sub-processes.
*Functions* therefore are defined in *.bashrc* / *.zshrc* files.

The example shows a *function* to shortcut *git stash* commands.
It accepts parameters: `+`, `.`, `push`, `--push` to push content
to the stash and: `x`, `pop`, `--pop` to extract.
Called with no argument, prints the stash list or that the stash
is empty.

```sh
function stash() {  # git stash support
    case "$1" in
    +|.|push|--push) shift; git stash push; echo "-- created:"; stash ;;
    x|pop|--pop)     shift; git stash pop $* ;;
    # default case:
    *)  [ "$(git stash list)" ] && git stash list || \
            echo "[stash empty]"
    esac
}
```

Use:

```sh
git stash list          # list stashed content
stash                   # calling the shortcut function instead
```

Although *functions* suggest similarity to *functions* in programming
languages, there are differences, e.g. regarding passing parameters as
*Shell* argument lists and that no "value" can be returned.

To emulate returning values, *functions* print results to `stdout`
in a *sub-Shell* `$()` and assign its output e.g. to a variable:

```sh
# concatenate arguments with separator passed as first argument
function build_path() {
    local sep=$1; shift     # local variable for separator
    local res=""            # local variable for result
    for arg in $*; do
        [ -z "$res" ] && res=$arg || res+=$sep$arg
    done
    echo $res               # print result to 'stdout'
}

# $() forks sub-shell to call function, assign 'stdout' to result variable
result=$(build_path ":" /bin /usr/bin /usr/local/bin)
echo PATH=\"$result\"
```
```
PATH="/bin:/usr/bin:/usr/local/bin"
```

&nbsp;

Building a Windows `PATH` that uses `[;]` as separator:

```sh
# using ';' as path separator
echo WIN_PATH=\"$(build_path ";" /bin /usr/bin /usr/local/bin)\"
```
```
WIN_PATH="/bin;/usr/bin;/usr/local/bin"
```



