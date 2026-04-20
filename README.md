<!-- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -->
<!-- A1 (SE-2)
-->
# A1 - A5 : Setup

<!-- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -->

Goal of the following assignments is to set-up your laptop for
software development:

1. [A1: *Laptop/Terminal* - Setup](#a1-laptopterminal---setup) - 5 Pt

1. [A2: Understanding the *Terminal*](#a2-understanding-the-terminal) - 5 Pt

1. [A3: *Java* - Setup](#a3-java---setup) - 5 Pt

1. [A4: *git* - Setup](#a4-git---setup) - 5 Pt

1. [A5: *VSCode* - Setup](#a5-vscode---setup) - 5 Pt


<!-- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -->

&nbsp;

## A1: *Laptop/Terminal* - Setup

The terminal is the primary tool to interact with computers in software
development. *Mac* or *Linux* laptops have proper terminal software installed.
*Windows* laptops require Unix-compatible terminal emulator software.
Test your laptop that it has proper terminal software and install, if not.

**`->` Mac:**

- Read article by *Thomas Auinger:*
    [*"Setting up my new MacBook Air M3 for Java Development"*](https://medium.com/@thomas.auinger/setting-up-my-new-macbook-air-m3-for-java-development-fc609af738cb) and
    install:

    - the *Homebrew* [*brew*](https://brew.sh) package manager (if not already):

        ```sh
        /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
        ```

    - Give user sudo-permissions (in order to install software from the terminal):

        ```
        sudo visudo
        ```

        Make sure the *%admin* entry appears as shown and add, if not:

        ```
        # User privilege specification
        root    ALL=(ALL) ALL
        %admin  ALL=(ALL) ALL
        ```

    - Install package [*coreutils*](https://formulae.brew.sh/formula/coreutils), which
        installs some needed *Unix* tools such as the *realpath* command.

    - Feel free to install other packages such as *"Tabby"* and *"Oh My Zsh"* for
        pretty prompts (although this is not needed).


**`->` Windows:**

- Follow steps in [*Setting up Cygwin*](10-Setup-cygwin.md) to install the
    [*cygwin*](https://www.cygwin.com) Unix-emulator. Mind specifically *step2* to:

    - switch from path prefix `/cygdrive/c` to `/c` and
    
    - change the *cygwin* *HOME*-directory from the installation path to a preferred
        location on your laptop (optional).


**`->` Linux:** -- you are all set.

&nbsp;

Test your configuration. Open a terminal and type:

```sh
# show real path to the current ('.') directory
realpath .      --> outputs path, e.g. /Users/thompson
                --> path on Windows must start with '/c', e.g. /c/Users/thompson

# show path of the 'HOME' directory
echo $HOME      --> /c/Sven1/svgr2

# change to the 'HOME' directory ('-l' long version)
cd

# show content of the 'HOME' directory ('-a' all file/directories)
ls -l

# show also 'dotfiles'
ls -la

# show content of the 'PATH' variable
echo $PATH
```


<!-- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -->

&nbsp;

## A2: Understanding the *Terminal*

Read [*Understanding the Terminal*](20-Understanding-the-Terminal.md) and learn
basic concepts or recall from the *Operating Systems* course.

Write-down short answers to questions:

1. What is a *shell*? - Name two *shells*.

1. What is *PATH*?

1. What is a (system-) process?

1. Draw basic processes involved in running a terminal application.

1. What is *UTF-8*? - How many bytes are needed to represent character *"A"* and *"€"* ?

1. What are *CR/LF* and *NL*? - What is the problem with *CR/LF* ?

1. Who is *Ken Thompson*?


Open a terminal and type:

```sh
# show content of the current directory ('-a' all file/directories)
ls -l

# show also 'dotfiles'
ls -la
```

What do you see?

```
$ ls -la
total 121
drwxr-xr-x 1 svgr2 Kein     0 Apr  6 18:21 .
drwxr-xr-x 1 svgr2 Kein     0 Aug  3  2024 ..
-rwxr-xr-x 1 svgr2 Kein 12907 Nov 13 15:44 .bashrc
-rw-r--r-- 1 svgr2 Kein  1117 Oct 15 17:59 .gitconfig
-rwxr-xr-x 1 svgr2 Kein 21529 Oct  9 18:54 .profile
drwxr-xr-x 1 svgr2 Kein     0 Oct  9 13:20 .ssh
-rw-r--r-- 1 svgr2 Kein  1056 Oct  9 18:21 .vimrc
-rw-r--r-- 1 svgr2 Kein   508 Oct  9 17:59 .zprofile
-rw-r--r-- 1 svgr2 Kein  1342 Oct  9 17:59 .zshrc
drwxr-xr-x 1 svgr2 Kein     0 Apr  6 18:27 workspaces
...
```

What does *'rwx'* mean?

Test your terminal that it properly handles *UTF-8* and *ANSI colors*.

```sh
echo "I won't pay 10€ for this."

echo -e "I won't pay 10\0342\0202\0254 (UTF-8 encoding) for this."

echo -e "Hello \033[31;1mWorld\033[0m - Hello \033[34;1mUniverse\033[0m !"
```

Output should show proper rendering of the *"€"* character:

```
I won't pay 10€ for this.
```

Coloring shows the effect of ANSI-code sequences.

<img src="img/terminal-3-hello-colors.png" width="600"/>

What is *"PS1"*?

How are [*"pretty prompts"*](https://wiki.archlinux.org/title/Bash/Prompt_customization)
created?


<!-- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -->

&nbsp;

## A3: *Java* - Setup

*Java* comes in two major variaties:

- *Java JRE* - Java Runtime Environment only includes the 

    - `java` Virtual Machine and libraries needed during runtime to run
        compiled Java programs.

- *Java SDK* - Java Software Development Kit includes the full set of Java tools:

    - `javac` - the Java compiler to compile Java source code in `*.java` files
        to [*Portable Byte Code*](https://en.wikipedia.org/wiki/List_of_JVM_bytecode_instructions)
        in `*.class` files that can be loaded and executed by the JavaVM.

    - `javadoc` - the Java documentation compiler that generates HTML-documentation from
        comments in Java source code.

    - `jar` - the Java archiver that packages `*.class` files into `*.jar` (Java archive)
        files for distribution.

Other varieties include:

- *Java SE* standard edition, which is the free implementation distributed by
    *Oracle* and with *Open-JDK* that only includes the standard Java libraries.

- [*Jakarta EE*](https://en.wikipedia.org/wiki/Jakarta_EE) enterprise edition or
    *Java EE* (former name), which is a large framework for commercial Java
    software development.


Java is an open language specification, which means multiple implementations
exist, most prominently:

- [*Java from Oracle*](https://www.oracle.com/java) -
    [*Oracle*](https://en.wikipedia.org/wiki/Oracle_Corporation) is a dominat
    US data- and database company that aquired Java from *Sun Microsystems*
    in 2010 and owns Java.

- [*Open-JDK*](https://openjdk.org) is an open-source implementation of the
    Java Platform, Standard Edition (Java SE).

The [*Java Version history*](https://en.wikipedia.org/wiki/Java_version_history)
dates back to Jan 23, 1996 with *JDK 1.0*.

- *Java 26 SE* was released on March 17, 2026

- *LTS* (Long-term support) releases are *Java SE 21 (LTS)* and *Java SE 25 (LTS)*.

New *Java* releases often cause problems with existing code and libraries,
see example
[*"Unable to compile using java 25 \#3949"*](https://github.com/projectlombok/lombok/issues/3949)
for problems of *Java 25* with the [*lombok*](https://projectlombok.org/) library.

It is *adviced* to use the stable *Java 21* for the course. The more adventurous can
try the latest *Java*.

Verify your *Java* installation and install, if needed:

**`->` Mac:** - follow steps in article [*"Install Java on macOS"*](https://www.baeldung.com/java-macos-installation#using-homebrew-package-manager)
    using *brew* (mind to choose Java not older than *Java 21*, which is preferred).

**`->` Windows:** - download
    [*x64 installer*](https://www.oracle.com/de/java/technologies/downloads/#jdk21-windows)
    and install *Java*.

**`->` Linux:** - follow steps in article [*"ava auf Linux installieren"*](https://docs.fabricmc.net/de_de/players/installing-java/linux) depending on your *Linux* distribution.


&nbsp;

Test: open a terminal and show that tools are installed with proper (same) versions:

```sh
java --version          --> java 21 2023-09-19 LTS

javac --version         --> javac 21

javadoc --version       --> javadoc 21

jar --version           --> jar 21
```

Verify the Java - installation path is set to the *JAVA_HOME* environment variable:

```sh
echo $JAVA_HOME         --> /c/Program Files/Java/jdk-21
```

Create file `HelloWorld.java` in a directory: `~/workspaces/hello-world`
(`~` refers to the *HOME*-directory):

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

Compile and execute:

```sh
cd                                  # change to your HOME directory

mkdir -p ~/workspaces/hello-world   # make (mk) directories

cd workspaces/hello-world           # change into the 'hello-world' directory

# print the working directory
pwd                         --> /c/Sven1/svgr2/workspaces/hello-world

# create file '' in the directory - use an editor or IDE
...

cat HelloWorld.java         --> output the file content

# compile file 'HelloWorld.java'
javac HelloWorld.java       --> Java compiler creates file 'HelloWorld.class'

# run 'HelloWorld.class'
java HelloWorld             --> 'Hello, World!'
```


<!-- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -->

&nbsp;

## A4: *git* - Setup

[*Git*](https://git-scm.com) is a widely used
[*source-code management*](https://en.wikipedia.org/wiki/Comparison_of_version-control_software)
tool developed by *Linus Torvalds* for the large-scale, distributed development
of the *Linux*-kernel released in 2005.

*git* is primarily a ***local tool***. Test you have the local tool *git* installed:

```sh
git --version               --> git version 2.48.1.windows.1
```

[*GitLab*](https://en.wikipedia.org/wiki/GitLab) e.g.
[*https://gitlab.bht-berlin.de*](https://gitlab.bht-berlin.de) or
[*GitHub*](https://en.wikipedia.org/wiki/GitHub) (owned by *Microsoft*)
are ***services*** that are hosted on the network and are used to share code
with other developers by *pushing* and *pulling* local commits.

File [*.gitconfig*](https://github.com/sgra64/dotfiles/blob/main/.gitconfig)
in the user's *HOME* directory stores *git* user-settings. Those settings are
valid for all *git* projects a user has on a laptop.
File *.gitconfig* is created when a local *git* repository is initialized for
the first time.

Put project `hello-world` under git control :

```sh
cd ~/workspaces/hello-world         # change into the 'hello-world' directory

ls -la                              # show the content of the project directory
```
```
total 6
drwxr-xr-x 1   0 Apr  6 22:15 ./
drwxr-xr-x 1   0 Apr  6 22:14 ../
-rw-r--r-- 1 427 Apr  6 22:15 HelloWorld.class
-rw-r--r-- 1 123 Apr  6 21:40 HelloWorld.java
```

Initialize the project directory as *git* project:

```sh
# create new git project
git init --initial-branch=main      # initialize new local git repository
```

If you have never created a local *git* repository on your laptop, you may be
asked to create a local *git* configuration file first.
File [`$HOME/.gitconfig`](https://github.com/sgra64/dotfiles/blob/main/.gitconfig)
is created in your *HOME*-directory with commands:

```sh
git config --global user.name "your name"
git config --global user.email "your@email.com"
```

Show content of file *$HOME/.gitconfig*:

```sh
cat $HOME/.gitconfig        # show '.gitconfig' file
```
```
[user]
    name = Sven Graupner                <-- your name
    email = sgraupner@bht-berlin.de     <-- your email address

[core]
    ignorecase = true       # ignore upper/lower case in file names
    autocrlf = false        # disable crlf conversion on checkout
    filemode = false        # ignore filemode (rwx) changes
    eol = lf                # always use newline '\n' as end-of-line

[init]
        defaultBranch = main
```

**Important:** specifically for *Windows* laptops, put entries under `[core]`
and `[init]` into your *$HOME/.gitconfig* file.

Back to the *se1-play* project. Show the project content with the new local
*git* repository:

```sh
ls -la                              # show the content of the project directory
```
```
total 14
drwxr-xr-x 1   0 Apr  6 22:17 ./
drwxr-xr-x 1   0 Apr  6 22:14 ../
drwxr-xr-x 1   0 Apr  6 22:17 .git/             <-- new directory with git repository
-rw-r--r-- 1 427 Apr  6 22:15 HelloWorld.class
-rw-r--r-- 1 123 Apr  6 21:40 HelloWorld.java
```

Next, create an empty root commit and tag as *"root"*:

```sh
git commit --allow-empty -m "root commit (empty)"       # create empty root commit
git tag root                                            # tag commit as 'root'

git log --oneline                                       # show the new commit
```
```
e9c43c5 (HEAD -> main, tag: root) root commit (empty)   <-- empty root commit
```

Next, create two commits:

- an empty *root commit* - adviced as start of a new *git* repository.

- a commit with file `HelloWorld.java`

```sh
# create first (empty) commit and tag as 'root' commmit
git commit --allow-empty -m "root commit (empty)"
git tag root

git log --oneline               # show commit history
```
```
b301f93 (HEAD -> main, tag: root) root commit (empty)   <-- one commit on branch 'main'
```

Verify the *git* status of the project:

```sh
git status                      # show git status of the project
```

Files in red are marked as *untracked files* (unknown to *git*):

<img src="img/git-1.png" width="600"/>


&nbsp;

Next, we want to create a second commit on branch *main* that contains file
`HelloWorld.java`.

A *"commit"* is a *set (snapshot) of files* that is recorded on a branch, here
branch: *main*. A commit is always added at the end of a branch after a
preceeding commit. A *branch* hence is a linear sequence of recorded commits.

Commits are created in two steps in *git*:

1. *"staging"* - a step that defines the set of files to be committed.
    During *staging*, files can be added or removed to/from the so-called
    *staging area* in the local repository that is defining the files for
    the upcomming commit. No commit is created during *staging* nor other
    harm can be done.

2. *"commit"* - all files from the *staging area* are bundled as a snapshot,
    assigned a unique *commit-ID* and appended at the end of the current branch.
    The *staging area* is cleared.

Step 1 *"staging"* is performed by the `git add` and `git reset` commands that
add or remove files to/from the *staging area*:

```sh
# stage file 'HelloWorld.java'
git add HelloWorld.java

# show git status of the project after staging file 'HelloWorld.java'
git status
```

<img src="img/git-2.png" width="600"/>

Command: `git reset HelloWorld.java` removes the file from the *staging area*,
with `add`, the file can be added again.

Committing the snapshot of files (only one file here) with message:

```sh
# commit all staged files with message (-m)
git commit -m "added source file HelloWorld.java"

git log --oneline               # show the commit history (short)
git log                         # show the commit history (full)
```

The commit-log now has two commits.
*Commit-ID* are shown in a short 7-digit version (`7b46019`).

<img src="img/git-3a.png" width="600"/>

The long-form of the commit-log shows more detail, including the full 40-digit
 *commit-ID* (`7b46019...`).
*HEAD* points to the last (top) commit  of the *main* branch indicating the
commit the project directory (*"working tree"*) is synchronized with. 

<img src="img/git-3b.png" width="600"/>

The next command shows the difference between the current (last) commit
addressed by `HEAD` and the previous commit addressed by `HEAD~1`
(read: *HEAD* minus 1, the tilde sign `'~'` is used for minus since `'-'`
has other effects in shell commands):

```sh
git diff HEAD~1..HEAD --name-status
```
```
A       HelloWorld.java         <-- 'A' means file 'HelloWorld.java' was added
```

Add *Javadoc* to file `HelloWorld.java`:

```java
/**
 * Class with static {@code main(String[] args)} function that
 * prints the {@code "Hello, World!"} message.
 */
public class HelloWorld {

    /**
     * Print the {@code "Hello, World!"} message.
     * @param args arguments passed from the command line
     */
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

Create the *HTML* from the doc-Strings using the `javadoc` compiler:

```sh
javadoc -d javadoc HelloWorld.java      # generate java documentation in directory 'javadoc'

ls -la                                  # show content of the project directory
```
```
total 26
drwxr-xr-x 1   0 Apr  6 23:37 ./
drwxr-xr-x 1   0 Apr  6 22:14 ../
drwxr-xr-x 1   0 Apr  6 23:27 .git/
-rw-r--r-- 1 427 Apr  6 22:15 HelloWorld.class
-rw-r--r-- 1 367 Apr  6 23:25 HelloWorld.java
drwxr-xr-x 1   0 Apr  6 23:37 javadoc/          <-- new directory with HTML
```

The result is in a new directory (`-d`) `javadoc` in the project directory.
Open file `javadoc/index.html` in a browser to see the created documentation:

<img src="img/javadoc-1.png" width="600"/>

&nbsp;

Checking the status of the project, we find that the project has *"dirty state"*
after the modification of file `HelloWorld.java`:

```sh
git status                              # show status of the project directory
```

<img src="img/git-4.png" width="600"/>

Commit the change made in file `HelloWorld.java`.

```sh
git log --oneline                     `# show status of the project directory
```
```
2527ce7 (HEAD -> main) added Javadoc to HelloWorld.java     <-- third commit
7b46019 added source file HelloWorld.java
b301f93 (tag: root) root commit (empty)
```

Keeping seeing files that are not recored by commits in red as *"untracked"* is
bothering and even dangerous for accidental commits, particularly when using
shortcut `git add .` referring to *"all"* modified of untracked files.

Learn about special file
[*.gitignore*](https://www.w3schools.com/git/git_ignore.asp)
and create one that prevents:

- file `HelloWorld.class` and

- directory `javadoc`

from being shown as *"untracked"* and to be ignored by *git* in future.

Commit file `.gitignore` as fourth commit:

```
0ba3580 (HEAD -> main) add .gitignore       <-- 4th commit, message "add .gitignore"
2527ce7 added Javadoc to HelloWorld.java
7b46019 added source file HelloWorld.java
b301f93 (tag: root) root commit (empty)
```

&nbsp;

Validate your `~/.gitconfig` file in your HOME directory with the example,
particularly for *Windows* settings: `ignorecase`, `autocrlf`, `filemode`
and `eol` must be set:

```
# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
# Global git settings in $HOME/.gitconfig apply to all git projects of a user.
# Additional project settings are stored in the project's .git directory under
# <proj-dir>/.git/config.
# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

# Validate name and email in the [user] section by editing or by commands:
# - git config --global user.name "your name"
# - git config --global user.email "your@email.com"
# 
[user]
    name = Eric Meyer
    email = emey@bht-berlin.de

[core]
    ignorecase = true       # ignore upper/lower case in file names
    autocrlf = false        # disable crlf conversion on checkout
    filemode = false        # ignore filemode (rwx) changes
    eol = lf                # always use newline '\n' as end-of-line

[init]
    defaultBranch = main
```


&nbsp;

Perform the final test:

```sh
ls -la
git status
git log --oneline
```

Expected output:

```
$ ls -la
total 27
drwxr-xr-x 1 svgr2 Kein   0 Apr  6 23:58 .
drwxr-xr-x 1 svgr2 Kein   0 Apr  6 22:14 ..
drwxr-xr-x 1 svgr2 Kein   0 Apr  6 23:58 .git
-rw-r--r-- 1 svgr2 Kein  17 Apr  6 23:58 .gitignore
-rw-r--r-- 1 svgr2 Kein 427 Apr  6 22:15 HelloWorld.class
-rw-r--r-- 1 svgr2 Kein 367 Apr  6 23:25 HelloWorld.java
drwxr-xr-x 1 svgr2 Kein   0 Apr  6 23:37 javadoc

$ git status
On branch main
nothing to commit, working tree clean       <-- clean "working tree"

$ git log --oneline
0ba3580 (HEAD -> main) add .gitignore
2527ce7 added Javadoc to HelloWorld.java
7b46019 added source file HelloWorld.java
b301f93 (tag: root) root commit (empty)
```
<!-- 
<img src="img/git-5.png" width="600"/>
-->

Take notes and answer questions:

1. Where is a local *.git* repository stored?

1. What is a *commit*?

1. What is a *branch*? - What is branch *main*?

1. Why was file `HelloWorld.java` commited, `HelloWorld.class` and directory
    `javadoc` not?

1. What do people mean saying that the project directory is in a *"clean state"*
    or they have a *"clean project directory"* `->` you may ask your AI to find out.

1. When is a *project state* *"dirty"* (you can't switch branches in *dirty state*).
    How can *"dirty state"* be cleaned up?

1. Can commits be changed after they have been committed (e.g. files added,
    the commit-message changed or the commit-id)?


<!-- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -->

&nbsp;

## A5: *VSCode* - Setup

[*Visual Studio Code (VSCode)*](https://code.visualstudio.com) by *Microsoft* is a modern,
popular *IDE* (Integrated Development Environment) with:

- Multiple programming languages support (*"polyglot"*).

- A large choice of extensions (e.g. *"Java extension pack"*, *"Code Runner"* extension).

- Ability to develop in remote environments (cloud, containers) over the network.

- Built-in *AI integration* (Microsoft's *Co-Pilot*) or through extensions, e.g. *Claude*
    and others.


For this course, following *VSCode* extensions need to be installed:

- [*Extension Pack for Java*](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack) -- required.

- [*Code Runner*](https://marketplace.visualstudio.com/items?itemName=formulahendry.code-runner) -- recommended.

`->` Make sure you can start *VSCode* from the terminal, e.g. by setting *PATH* in
`.bashrc`.

`->` *VSCode* opens each project separately (not multiple projects or entire
workspaces at once, which is in contrast to older *IDE* such as *eclipse*).

`->` Hence, *VSCode* must be started from within the project directory.

Navigate to the project directory and start *VSCode*:

```sh
cd ~/workspaces/hello-world         # cd to into the project directory

code .                              # start VSCode in this '.' (dot) current directory
```

*VSCode* will open and show project files.

Run the *HelloWorld* Program with:

- the internal *launcher* (see screenshot) or with

- *Code Runner* that is activated by (default): `<Ctrl> + <Alt> + N`

Output of the program should appear in the integrated Terminal panel (launcher) or
in the Output panel (Code Runner).

&nbsp;

<img src="img/vscode-1.png" width="800"/>


