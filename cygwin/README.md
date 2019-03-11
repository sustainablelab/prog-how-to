# Installation
## Cygwin
### Install a fresh Cygwin
- On the computer to setup Cygwin, install Cygwin. Download the setup from
  <https://cygwin.com/install.html>. The file is called `setup-x86_64.exe`.
  Cygwin is a package manager for all the tools that make up a Cygwin
  installation. The setup downloads the Cygwin packages to the *Downloads*
  folder by default, which is fine.
- I like to download from `mirror.clarkson.edu(http)`.
- Change the *View* to *Pending*. This shows the base installation.
- The installation goes quickly. When it is done, the desktop shortcut opens a
  POSIX terminal. Run `pwd` to view the present working directory.
```bash
$ pwd
/home/Demos and DF
```
- This `home` folder is in `C:\cygwin64\`.
- four *dot files* are created:
    - `.bash_profile`
    - `.bashrc`
    - `.inputrc`
    - `.profile`
- If `Demos and DF` (the user *Home* folder) does not exist, launching Cygwin
  creates it.

### Reproduce an existing installation
I reproduce my existing Cygwin installation on the new computer by restoring
from a backup of my existing Cygwin installation.

#### Backup the Cygwin to copy
- make the backup by saving 'mount points':
```bash
mount -m > /usr/bin/mountCommands.bat
```

- the above command writes to this file:
```powershell
C:\cygwin64\bin\mountCommands.bat
```

#### Put the zipped copy on Dropbox
- Save the `C:\cygwin64` directory on Dropbox at:
```powershell
`C:\chromation-dropbox\Dropbox\c\cygwin64`
```

- To save space on my local drive, I don't keep this folder synced in Dropbox
  because it is 4GB unzipped, 1.5GB zipped. Therefore, delete this from the web
  client or from a local drive on a machine that *does* Dropbox-sync this
  folder, like the *dogfood* laptop.
- Now no one is synced to this folder because it does not exist on Dropbox
  anymore.

#### Grab the zip file from Drobox, unzip, and move to the Cygwin folder
- Do not install Cygwin on the computer to setup Cygwin. You can, but it is a
  wasted effort. Just copy the cygwin64.zip from Dropbox, unzip, and move the
  contents into `C:\cygwin64\`.

#### Match user names if possible
When Cygwin runs, it runs the dot files in the `home` sub-folder that matches
the Windows user name.

If the Windows user name is `Mike`, the `home` folder in `C:\cygwin64\` contains
a `Mike` folder with all of Mike's dotfiles and other local stuff.

If `Mike` does not exist, Cygwin creates a `Mike` folder with the default
dotfiles.

So it is easiest to rebuild the Cygwin setup on a new machine if that machine
has the same user name. Some Windows editions allow multiple user accounts, some
do not.

If the user name must be different, just delete any existing default content in
that folder and copy in from the existing installation. For example, `Demos
and DF` is the user name on the *dogfood* laptop, so I can give user `Demos and
DF` my Cygwin mojo by moving in the contents of the `Mike` folder in the
cygwin64.zip (copied from Dropbox). I ended up not doing this and just making a
`Mike` user account.

#### The Windows User creates their own home sub-folder
- About the folders in `C:\cygwin64\`
    - log in as `Mike` to create the `Mike` sub-folder
    - log in as `Demos and DF` to create the `Demos and DF` sub-folder
- if `Demos and DF` creates the `Mike` sub-folder, then user *Mike* does not
  have access to write the files there!
- Some files should have read-only access, and Windows considers the `Mike`
  sub-folder read-only, but *Mike* must be able to write files as well.
    - For instance, NERDTree has a Bookmarks file that it needs write-access
      too. To create a Vim session file, you need write-access in this folder.
      The simplest way to get the write combination of permissions is for the
      Windows User to create the sub-folder.
#### The Windows User unzips the transplanted cygwin64.zip
- If the Cygwin installation is transplanted from an existing installation on
  another machine, a Windows user gets the correct permissions by being the one
  to unzip the cygwin64.zip file.
- I actually tested this and confirmed it.
- When `Demos and DF` unzips the file, it owned the `home\Mike` folder. When
  `Demos and DF` launches the Cygwin terminal, there are no error messages
  because it can write to the `home\Mike` folder. Since the names are different,
  however, a `Demos and DF` folder is created and the skeleton dotfiles are
  placed there.
- When `Mike` tries to launch Cygwin, there are numerous errors that I think all
  trace back to Mike having read-only access to all files in the `home\Mike`
  folder. And since the name matches, a new sub-folder is *not* created, and
  then the errors are generated.
- When `Mike` unzips the file, `Mike` owns the `home\Mike` folder. When `Mike`
  launches Cygwin there are no errors.
- The problem is that only one user can be the one to unzip the folder. I had to
  have `Demos and DF` erase the entire copy of cygwin64 and then user `Mike`
  place the version unzipped by `Mike`.

### Mintty
- Mintty is the default Cygwin terminal.
- Cygwin places a shortcut to launch the Cygwin terminal on the Windows Desktop.
- Alternatively, I prefer to launch *Mintty* from the Windows PowerShell.
- [ ] list the changes I made to the default *Mintty* terminal.

### X11 Setup
#### Context for X11
Linux windows management is a modular system known as `X`. `X11` is `11` because
that was the final stable version from MIT back in the late 1980s.

This is the low-level on top of which are built the many different Linux Window
Managers: KDE, GNOME, tvm, etc.

#### Cygwin/X is part of default Cygwin Installation
At a minimum, I think you need Cygwin packages `xinit` and `xterm`. But the
minimum installation is already part of the default Cygwin installation.

#### Install additional Cygwin/X packages with Cygwin Package Manager
View all of the `X11` packages by opening the Cygwin package manager and setting
the view to `Category`, and expanding the last item, `X11`. Install utility
`xclock` to have something to test that the system is working.

Besides `Category`, also do a direct search for a few things.
Search for `xhost`, `xinit`, and `xorg`. Grab whatever looks useful, especially
the `font` related packages.

### X11 Usage
It is not obvious how to *use* X11. There is an assumed knowledge of what X11 is
doing, which certainly was not obvious to me.

At a minimum, to have a display device where SDL can open a window, you need to:
- start an X Window server
- start a windows manager

See the user guide:
<https://x.cygwin.com/docs/ug/using.html>

#### xwin
Run `xwin` to start an `XWin X Server`. Run this in the background with `&` to
continue using the `bash` terminal for running X11 applications to be displayed
in the `XWin`.

```bash
$ xwin &
```

A black window opens with title bar `Cygwin/X:0.0`.
The following stream is output to the original `bash` terminal.

```bash
[1] 5880

Mike@ChromationMJG ~
$ Welcome to the XWin X Server
Vendor: The Cygwin/X Project
Release: 1.20.2.0
OS: CYGWIN_NT-6.3 ChromationMJG 2.11.2(0.329/5/3) 2018-11-08 14:34 x86_64
OS: Windows 8.1  [Windows NT 6.3 build 9600] (Win64)
Package: version 1.20.2-1 built 2018-10-24

winInitializeScreenDefaults - primary monitor w 1920 h 1080
winInitializeScreenDefaults - native DPI x 96 y 96
XWin was started with the following command line:

xwin

(II) xorg.conf is not supported
(II) See http://x.cygwin.com/docs/faq/cygwin-x-faq.html for more information
LoadPreferences: /home/Mike/.XWinrc not found
LoadPreferences: Loading /etc/X11/system.XWinrc
LoadPreferences: Done parsing the configuration file...
winDetectSupportedEngines - RemoteSession: no
winDetectSupportedEngines - DirectDraw4 installed, allowing ShadowDDNL
winDetectSupportedEngines - Returning, supported engines 00000005
winSetEngine - Using Shadow DirectDraw NonLocking
winScreenInit - Using Windows display depth of 32 bits per pixel
winWindowProc - WM_SIZE - new client area w: 1904 h: 1001
winFinishScreenInitFB - Masks: 00ff0000 0000ff00 000000ff
MIT-SHM extension disabled due to lack of kernel support
XFree86-Bigfont extension local-client optimization disabled due to lack of shared memory support in the kernel
(EE) AIGLX: No native OpenGL in modes with a root window
(II) IGLX: Loaded and initialized swrast
(II) GLX: Initialized DRISWRAST GL provider for screen 0
winPointerWarpCursor - Discarding first warp: 952 500
(--) 16 mouse buttons found
(--) Setting autorepeat to delay=500, rate=31
(--) Windows keyboard layout: "00000409" (00000409) "US", type 4
(--) Found matching XKB configuration "English (USA)"
(--) Model = "pc105" Layout = "us" Variant = "none" Options = "none"
Rules = "base" Model = "pc105" Layout = "us" Variant = "none" Options = "none"
````

#### xterm needs a DISPLAY
`xterm` does not work out of the box:
```bash
$ xterm
```
This outputs an error that the display cannot open:
```
xterm: Xt error: Can't open display:
xterm: DISPLAY is not set
```
`xterm` needs to know which *display server*(?) to run on. The local display is
always `:0.0`. I think the display server is indicated in the title bar of the
`XWin`.
Set the `DISPLAY` variable:
```bash
export DISPLAY=:0.0
```
`export` makes the DISPLAY variable *persist in the environment*(?).

Put the `export` line in your `.bashrc` to set this variable for good.

Now `xterm` and any other `X11` applications know where the `DISPLAY` is.

#### launch X11 applications from the xterm
Launch an `xterm` to get started. Again, run with `&` to run the process in the
background so that the `bash` terminal is still available for use while the
process runs.
```bash
$ xterm &
```
This outputs:
```bash
[2] 5888

$ winProcEstablishConnection - winInitClipboard returned.
winClipboardThreadProc - DISPLAY=:0.0
OS maintains clipboard viewer chain: yes
winClipboardProc - XOpenDisplay () returned and successfully opened the display.
xterm: cannot load font "-Misc-Fixed-bold-R-*-*-13-120-75-75-C-120-ISO10646-1"
```

The error message `cannot load font` is a common bug at the moment. Don't worry
about it, it will go away sooner or later when the `X11` packages are updated.

```bash
winWindowProc - WM_SIZE - new client area w: 1904 h: 1001
winWindowProc - WM_EXITSIZEMOVE
```
The `winWindowProc` lines show up in `bash` *every time* something happens in
the `XWin`. I wonder if there is a way to silence this.

At this point you can continue spawning `X11` processes in the background from
`bash` and they will show up in the `XWin`, or you can spawn them from the
`xterm`. To type in the `xterm`, the mouse must hover over the `xterm` window.

For example, try `X11` application `gerbv`.

#### gerbv
I built `gerbv` from source on Cygwin and was disappointed when it didn't run. I
had no idea it required `X11`. It uses `Gtk` and I think `Gtk` depends on `X11`.

I gave up and installed the pre-built Windows static binary, but it turns out,
all I needed was `X11`! Now `gerbv` runs *no problem*, and this local build I
did following the instructions on the `gerbv` site runs much smoother than the
pre-built Windows binary.

Run `gerbv` from `bash` or from `xterm`. The result is the same.

Now I can save projects in `gerbv`, close `gerbv`, and re-open them later!

But there is an issue with permissions. When I save a file or try to open
recently used files, `gerbv` attempts to access `recently-used.xbel`:
```bash
(gerbv:12172): Gtk-WARNING **: Attempting to store changes into
`/home/Mike/.local/share/recently-used.xbel', but failed: Failed to create file
“/home/Mike/.local/share/recently-used.xbel.Y18FXZ”: No such file or directory
```
This is happening because Cygwin does not have permission to create this file. A
lot of applications use this file, so this is not just a `gerbv` thing. Fix it
now by creating the file.
```bash
$ mkdir ~/.local/share
$ touch ~/.local/share/recently-used.xbel
```
I had to create recently `.local` for a local Python site-packages folder to
hold packages I write myself. If `.local` does not exist yet, `mkdir -p` to
create the full folder path in one go.

Yes, now the *recently used* list is available in `gerbv` *open*. I have a
feeling the same will be true in all other `X11` applications.

### X11 Doc
```bash
$ find /usr -name '*xorg*'
```
This finds:
```
/usr/share/aclocal/xorg-macros.m4
/usr/share/doc/Cygwin/xorg-scripts-1.0.1.README
/usr/share/doc/xorg-cf-files
/usr/share/doc/xorg-docs
/usr/share/doc/xorg-scripts-1.0.1
/usr/share/doc/xorg-server
/usr/share/doc/xorg-util-macros
/usr/share/doc/xorg-x11-fonts
/usr/share/doc/xorgproto
/usr/share/man/man5/xorg.conf.5.gz
/usr/share/man/man5/xorg.conf.d.5.gz
/usr/share/pkgconfig/xorg-macros.pc
/usr/share/X11/xkb/rules/xorg
/usr/share/X11/xkb/rules/xorg.lst
/usr/share/X11/xkb/rules/xorg.xml
/usr/bin/xorg-backtrace
/usr/lib/X11/config/xorg.cf
/usr/lib/X11/config/xorg.tmpl
/usr/lib/X11/config/xorgsite.def
/usr/lib/X11/config/xorgversion.def
/usr/lib/xorg
```
Open the `README.txt` in the docs:
```bash
$ vim /usr/share/doc/xorg-docs/README.txt
```
And from Vim, with the cursor in the window with the .txt, launch the `HTML` doc
with `;html`.

This doc is not very helpful.

[-] Find a doc that says how to check if an `XWin` is running.

Or maybe I simply use `SDL_Init` for this!

[x] Find documentation on the *right way* to start an XWin Xserver. I've seen
*many* different methods: `xwin &`, `xinit`, `startxwin`

see `man X`, `man Xserver`, `man XWin`, `man XWinrc`, `man startxwin`

in particular, see `man X` section `STARTING UP`



