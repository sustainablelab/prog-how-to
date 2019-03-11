# Installation
## Cygwin
### Install a fresh Cygwin
- On the Windows computer to setup Cygwin, download the setup from
  <https://cygwin.com/install.html>. The file is called `setup-x86_64.exe`.
- This is the Cygwin package manager for all the tools that make up a Cygwin
  installation.
- The setup downloads the Cygwin packages to the *Downloads* folder by default,
  which is fine. I just leave it there.
- Run the package manager by double-clicking the `.exe`.
- Until *IPFS* becomes the intergalactic standard, I have to pick a server to
  download from. I like to download from `mirror.clarkson.edu(http)`.
- Change the *View* to *Pending*. This shows the base installation.
- The installation goes quickly.
- When it is done, I have a desktop shortcut that opens a `mintty` terminal.
- Open the terminal with the desktop shortcut.
- Run `pwd` to view the present working directory.
```bash
$ pwd
/home/MrBeardo
```
- This `home` folder is in `C:\cygwin64\`. Open that folder in Windows Explorer.
- four *dot files* are created:
    - `.bash_profile`
    - `.bashrc`
    - `.inputrc`
    - `.profile`
- If the user *Home* folder (my `/home/MrBeardo`) does not exist, the first
  launch of the Cygwin terminal creates it.

### Motivation
Cygwin provides a **POSIX** environment on Windows. That means you can use *GNU*
utilities without isolation from the Windows memory and file system.

A virtual box running Linux is great. I can run `apt-get` at the shell and just
get stuff done without going down a plumbing rabbit hole. But there are
drawbacks to running a virtual box.

Unlike a virtual Linux box, Cygwin is *just* the POSIX environment. The base
installation seems a bit crippled, but I think this is good. Using Cygwin has
forced me to learn the plumbing that I take for granted on my Ubuntu virtual
box, those magic one-liners from *Stack Overflow*. And it skirts the problem of
deciding how much hard-drive space to give up.

Beyond education, Cygwin enables me to use a Windows machine however I
please. In my case, I roll my own IDE for game development, going back to the
old UNIX concept of tying small utilities together to satisfy a need not
foreseen by the authors of the individual utilities.

`Vim`, `make`, `gcc`, `clang`, `doxygen`, `pandoc`, `git`, `ctags`, `cscope`.
Together these form an IDE with tag-jumping, auto-completion, auto-generated
documentation, pretty-print documentation, easy-to-run test suites, and version
control. And all is continuously customized to my needs as I figure out what I'm
doing.

Without Cygwin, I'd need to get a second computer running Linux for myself, and
on my Windows work machine, I'd bite the bullet and install Visual Studio.

With Cygwin, I can cross-compile, testing on my native Windows hardware using
the `minGW` compilers, which target Windows, and then testing on a X-Windows
server using the compilers that target Cygwin (both sets of compilers are
available through the Cygwin package manager). I know it's not a substitute for
building and testing on separate machines, but I think it keeps me from
accidental Windows platform lock-in while still being able to run Windows
executables on computers without Cygwin.

### Extra commentary for Cygwin skeptics
- Skepticism is healthy especially with our modern proliferation of tools and
  languages. If I lost you at `double-click`, please read on before you abandon
  Cygwin.
- Launch-by-click is a general I-am-using-Windows issue, not a Cygwin issue. My
  solution is to create a `PowerShell` alias for just about everything,
  including running the Cygwin package manager and launching `mintty`. I like
  my mouse... for doing CAD. And for playing *Hidden Folks* with my kids. Not
  for executing files.
- The Cygwin package manger is the equivalent of `apt-get` on Linux and
  `chocolately` in Windows `PowerShell`. Unlike those command line tools, the
  Cygwin package manager has a GUI. But there are command-line options if you
  need it:
  <https://stackoverflow.com/questions/9751845/apt-get-for-cygwin>
- Moving forward, I'll switch to `apt-cyg` to provide clear instructions on
  package installation to avoid tedious descriptions of the GUI click
  walk-through.
