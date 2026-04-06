# Setting up *Cygwin* on *Windows*

[Cygwin](https://www.cygwin.com) is a Unix-Emulator that provides a terminal
([mintty](https://mintty.en.lo4d.com/windows))
in which Unix commands can be executed on Windows using
[*bash*](https://en.wikipedia.org/wiki/Bash_(Unix_shell))
(*Bourne Again Shell*) as command-line interpreter.

*Bash* was developed in 1989 as a successor to the *Bourne Shell*
*[sh](https://en.wikipedia.org/wiki/Bourne_shell)*.

Example of a
[bash terminal](https://cdn.ttgtmedia.com/rms/onlineimages/REF_bash_command_line_3.jpg).

*Cygwin* is <span style="text-decoration:underline">not</span> a Unix system,
container or virtual machine (like
[WSL](https://learn.microsoft.com/en-us/windows/wsl/about)).
*Cygwin* emulates most (but not all) Unix system calls such that most Unix commands
can be used on Windows.

[GitBash](https://gitforwindows.org)
is an alternative to *Cygwin* that uses a different emulator
[MinGW](https://www.mingw-w64.org).
It has has some flaws (e.g. does not support symbolic links and performs strange
path conversions that may cause problems, seedirectory
[link](https://stackoverflow.com/questions/54258996/git-bash-string-parameter-with-at-start-is-being-expanded-to-a-file-path)).


&nbsp;
## Steps

1. [Step 1](#1-install-cygwin) - Install *Cygwin*

2. [Step 2](#2-configure-cygwin) - Configure *Cygwin*

    - switch from `/cygdrive/c` to `/c` and use Unix-rwx access (not Windows ACL)

    - select HOME-directory

3. [References](#3-references)


&nbsp;

## 1. Install Cygwin

1. Download the installer `setup-x86_64.exe` from
[https://www.cygwin.com/install.html](https://www.cygwin.com/install.html).


1. Run the installer `setup-x86_64.exe`.

    - select useful tools from packages (check boxes):
        - Editors/`vim` - visual editor,
        - Web/`wget` - web downloader,
        - Net/`curl` - web downloader.
        - --
        - Devel/`make` - build tool for *C* -- (*C*-development only),
        - Devel/`gcc/g++` - *C/C++* compiler tools set,
        - Devel/`git` - source code management,


&nbsp;

## 2. Configure Cygwin

1. Change *cygwin* default path `/cygdrive/c` to: `/c` and use Unix *rwx* - access
    (not Windows ACL):

    - navigate to the *cygwin* installation directory called `cygwin64`.

    - inside, edit `/etc/fstab` and replace line
        ```
        none /cygdrive cygdrive binary,posix=0,user 0 0

        with:
        none / cygdrive binary,posix=0,user,noacl 0 0
        ```


1. Add bash-user that works with Windows and create *bash* HOME directory.

    - Find out your Windows user name: <user_name>

    - Create or select a directory to use as HOME-directory for
      *bash*, e.g. your Windows HOME-directory `C:\Users\<user_name>`
      (but also any other directory you may create as HOME).

      Read
      [Change Cygwin home folder after installation](https://stackoverflow.com/questions/1494658/how-can-i-change-my-cygwin-home-folder-after-installation).

    - Edit file `/etc/nsswitch.conf`:
        - to use your Windows HOME-directory, comment line (put hash # in front)
            ```
            #db_home:
            ```
        - to use a different HOME directory `<path>`, enter
            ```sh
            db_home: /c/<path>      # e.g. db_home: /c/users/svgr
            ```


1. Create a terminal icon on your Desktop.

    - In the installation directory (`cygwin64`), navigate to `./bin`
        and find file
        [mintty.exe](https://en.wikipedia.org/wiki/Mintty),
        which is the terminal emulator executable.

    - Create a shortcut for *mintty.exe*
        (right-click file -> Create Shortcut -> On Desktop).
        The terminal icon appears on your desktop.


1. Open *mintty* terminal and test:

    ```sh
    $ whoami
    <user_name>         # your user name appears

    $ echo $HOME        # print path to HOME-directory
    <home_directory>    # output, e.g. /c/Users/svgr

    $ cd $HOME          # change into HOME-directory
    $ ls -la            # show content
    total 203
    drwxr-xr-x+ 1 svgr2 Kein      0 Oct  4 22:20 .
    drwxrwx---+ 1 svgr2 Kein      0 Jan  1  2022 ..
    -rw-------  1 svgr2 Kein  14476 Oct  4 22:20 .bash_history
    -rwxr-xr-x+ 1 svgr2 Kein   2717 Oct  4 20:28 .bashrc
    ...

    $ echo Hello >hello.txt     # create file hello.txt with content Hello
    $ ls -la                    # show new file exists in $HOME
    total 203
    -rw-r--r--  1 svgr2 Kein      6 Oct  7 23:38 hello.txt
    ...

    $ cat hello.txt             # output content of file
    Hello
    ```


1. Open Windows file explorer (
    [ ? ](https://geekflare.com/wp-content/uploads/2021/06/14-alternative-file-managers-to-replace-windows-10-file-explorer.jpg)
    ) and navigate to file `hello.txt`.
    Open the file by clicking (ending `.txt` should open the file with *notepad*).


1. Return to *bash* terminal:
    - change to HOME-directory and
    - show content of file `.bashrc` using a text editor:
        *[vim](https://www.vim.org)* (already installed with cygwin),
        *[nano](https://www.nano-editor.org)* or
        *[sublime](https://www.sublimetext.com)*
        are good choices.

        ```sh
        $ cd            # change to bash HOME-directory
        $ ls -la        # find file .bashrc
        total 203
        -rwxr-xr-x+ 1 svgr2 Kein   2717 Oct  4 20:28 .bashrc

        $ cat .bashrc   # output file .bashrc
        content of file .bashrc appears...
        ```


&nbsp;

## 3. References

More information:

- [Differences between Cygwin and MinGW](https://stackoverflow.com/questions/771756/what-is-the-difference-between-cygwin-and-mingw)

- [Change Cygwin HOME directory after installation](https://stackoverflow.com/questions/1494658/how-can-i-change-my-cygwin-home-folder-after-installation).
