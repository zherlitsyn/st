Fork of the suckless simple terminal (st) with my modifications.
----------------------------------------------------------------
[st](https://st.suckless.org/) is a simple terminal emulator for X.

![Example 0](https://github.com/zherlitsyn/st/blob/master/image0.png "Example 0")
![Example 1](https://github.com/zherlitsyn/st/blob/master/image1.png "Example 1")

Features
--------
Ligature support
Scroll back through terminal output
GTK theme variant selection (in config.h):

    const char *gtkthemevariant = "dark"; // or "light"

Requirements
------------
libxft 2.3.4 \
Fira Code https://github.com/tonsky/FiraCode

Installation
------------
Edit config.mk to match your local setup (st is installed into
the /usr/local namespace by default).

Afterwards enter the following command to build and install st (if
necessary as root):

    cd src
    make patch
    make
    make install

On arch-based systems just:

    makepkg -si

See the man page for additional details.
