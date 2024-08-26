### Introduction
This tutorial gather's heavily from other tutorials; most especially from the book "Programmers guide to ncurses" by Dan Gooking
### installation
this tutorial is current with NCurses version 5.5.+. We assumes that you’re using a UNIX-like operating system (Linux,
FreeBSD, Mac OS X, or some other OS based on UNIX), but you can windows as well via Cygwin.
I assume you can setup a project in your IDE of choice in order to get the code to run. Those kinds of instructions get out of date quickly so i wouldn't cover them in details.
To install `ncurses`, follow these steps based on your operating system:

#### **On Linux:**

1. **Using a package manager:**
   - **Debian/Ubuntu:**
     ```bash
     sudo apt-get update
     sudo apt-get install libncurses5-dev libncursesw5-dev
     ```
   - **Fedora:**
     ```bash
     sudo dnf install ncurses-devel
     ```
   - **Arch Linux:**
     ```bash
     sudo pacman -S ncurses
     ```

2. **From source:**
   If you need the latest version or a custom build:
   - Download the latest source code from the [official GNU Ncurses page](https://ftp.gnu.org/gnu/ncurses/).
   - Extract the tarball:
     ```bash
     tar -xvzf ncurses-<version>.tar.gz
     cd ncurses-<version>/
     ```
   - Configure, compile, and install:
     ```bash
     ./configure
     make
     sudo make install
     ```

#### **On macOS:**

1. **Using Homebrew:**
   ```bash
   brew install ncurses
   ```

2. **From source:**
   - Follow the same steps as for Linux using the source code from the GNU Ncurses page.

#### **On Windows:**

`ncurses` isn't natively supported on Windows. However, you can use it with environments like Cygwin or WSL (Windows Subsystem for Linux).

- **Using Cygwin:**
  - Install `ncurses` during the Cygwin setup process.
  
- **Using WSL:**
  - Install it in your Linux distribution inside WSL as you would on a regular Linux system:
    ```bash
    sudo apt-get install libncurses5-dev libncursesw5-dev
    ```

#### Prerequisites
You should already:
- Have basic C/C++ knowlegde (C mostly)
- know how to compile C/C++ programs, link libraries and in rare scenerios make use of Build Systems(optional)

### Curses or NCurses?
The Curses library of terminal control functions has been with UNIX since the early 1980s. As such, it was part of the older versions of UNIX, which required complex licenses and such to be used. NCurses is the New Curses software emulation of the original Curses and is available from the GNU folks at the Free Software Foundation. the computer system you’re using employs NCurses, not the original Curses. Because of that, we use NCurses to refer to the library and its functions.
<a>Next page</a> 