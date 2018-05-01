![nimf](https://2.bp.blogspot.com/-w7cG7ZgujU8/V5NjTwey5mI/AAAAAAAACV8/84Uo8bz8KN0H8deR0V_zk1_Yft4PoANEwCLcB/s1600/Screenshot%2Bfrom%2B2016-07-23%2B21%253A28%253A21.png)
  
  

**Nimf** is an input method framework which has a module-based client-server
architecture in which an application acts as a client and communicates
synchronously with the Nimf server via a Unix socket.

# **Nimf** provides:

  * Input Method Server:
    - nimf-daemon
  * Language Engines:
    - Chinese (based on libchewing, librime)
    - Japanese (based on anthy)
    - Korean (based on libhangul)
  * Service Modules:
    - Indicator (based on appindicator)
    - Wayland
    - XIM (based on IMdkit)
    - Preedit window
    - Candidate
  * Client Modules:
    - GTK+2, GTK+3, Qt4, Qt5
  * Settings tool to configure the Nimf:
    - nimf-settings
  * Development files:
    - C library and headers
    

# Downloads

Download latest snapshot of the current master branch

* Clone with HTTPS

```bash
    git clone https://github.com/cogniti/nimf.git
```

* Download tar.gz

```bash
    https://github.com/cogniti/nimf/archive/master.tar.gz
```


# Compiling and installing

* Compiling and installing in the usual way

If you are using im-config

```bash
./autogen.sh --with-im-config-data
```

Otherwise

```bash
 ./autogen.sh
make
sudo make install
sudo ldconfig
sudo make update-gtk-im-cache
sudo make update-gtk-icon-cache
```

* Compiling and installing in Debian way

First of all, install devscripts, build-essential, debhelper.

```bash
$ sudo apt install devscripts build-essential debhelper
```

After installing devscripts, build-essential perform the following commands.

```bash
username:~$ cd
username:~$ mkdir tmp-build
username:~$ cd tmp-build
username:~/tmp-build$ wget https://github.com/cogniti/nimf/archive/master.tar.gz
username:~/tmp-build$ tar zxf master.tar.gz
username:~/tmp-build$ cd nimf-master
username:~/tmp-build/nimf-master$ dpkg-checkbuilddeps
```

You may see something like:

```bash
dpkg-checkbuilddeps: Unmet build dependencies: some-package1 some-package2
```

Install all dependent packages and perform the following commands.

```bash
username:~/tmp-build/nimf-master$ debuild
username:~/tmp-build/nimf-master$ cd ..
username:~/tmp-build$ ls
nimf_YYYY.mm.dd_amd64.build
nimf_YYYY.mm.dd_amd64.buildinfo
nimf_YYYY.mm.dd_amd64.changes
nimf_YYYY.mm.dd_amd64.deb
nimf_YYYY.mm.dd.dsc
nimf_YYYY.mm.dd.tar.xz
nimf-anthy_YYYY.mm.dd_amd64.deb
nimf-anthy-dbgsym_YYYY.mm.dd_amd64.deb
nimf-chewing_YYYY.mm.dd_amd64.deb
nimf-chewing-dbgsym_YYYY.mm.dd_amd64.deb
nimf-dbgsym_YYYY.mm.dd_amd64.deb
nimf-dev_YYYY.mm.dd_amd64.deb
nimf-libhangul_YYYY.mm.dd_amd64.deb
nimf-libhangul-dbgsym_YYYY.mm.dd_amd64.deb
nimf-master
nimf-rime_YYYY.mm.dd_amd64.deb
nimf-rime-dbgsym_YYYY.mm.dd_amd64.deb
```

Install *deb packages*.

```bash
$ sudo dpkg -i nimf_YYYY.mm.dd_amd64.deb \
  nimf-anthy_YYYY.mm.dd_amd64.deb nimf-chewing_YYYY.mm.dd_amd64.deb \
  nimf-libhangul_YYYY.mm.dd_amd64.deb nimf-rime_YYYY.mm.dd_amd64.deb
```

As above mentioned, make the package yourself. Otherwise, request your Linux
distribution to package Nimf.


# Configure

* For GNOME Shell, use 3rd party gnome-shell-extension-appindicator
    - https://extensions.gnome.org/extension/1031/topicons/
    - https://github.com/phocean/TopIcons-plus

* Configure Hangul/Hanja key if you use a keyboard without hardware Hangul/Hanja key
    - If you are using xkb-data 2.14 or newer, then select "Right Alt as Hangul, right Ctrl as Hanja" or "Right Ctrl as Hangul, right Alt as Hanja" from
    `gnome-tweak-tool`.


# Debugging

```bash
nimf-daemon --start-indicator --debug
tail -f /var/log/daemon.log
export GTK_IM_MODULE="nimf"
export QT4_IM_MODULE="nimf"
export QT_IM_MODULE="nimf"
export XMODIFIERS="@im=nimf"
export G_MESSAGES_DEBUG=nimf
gedit # or kate for Qt
```

# Participate

* Development
    - You may send pull requests.
    - https://github.com/cogniti/nimf/pulls

* Translation
    - You can make nimf.pot using the following commands.
    ```bash
      git clone https://github.com/cogniti/nimf.git
      cd nimf
      ./autogen.sh
      cd po
      make nimf.pot
    ```
    Then, you may translate nimf.pot into your native language.


# Support

* Not Nimf bugs but your application bugs
    - Report bugs to your application project. Do not request me to fix your application bugs.
* Failed to load shared library
    - Check /etc/ld.so.conf and /etc/ld.so.conf.d/ for /usr/local/lib path
* libnimf.so.0: cannot open shared object file: No such file or directory

```bash
sudo ldconfig
```
        
* Nimf does not appear in im-config

```bash
sudo cp nimf/data/im-config/23_nimf.* /usr/share/im-config/data/
```

# References

* APIs
    - http://www.x.org/releases/X11R7.6/doc/libX11/specs/XIM/xim.html
    - http://www.w3.org/TR/ime-api/
    - https://developer.chrome.com/extensions/input_ime
    - https://docs.enlightenment.org/stable/efl/group__Ecore__IMF__Lib__Group.html
    - http://doc.qt.io/qt-4.8/qinputcontext.html
    - http://doc.qt.io/qt-5/qinputmethod.html
    - https://git.gnome.org/browse/gtk+/tree/gtk/gtkimcontext.c

* Language Engines (alphabetically listed)
    - http://anonscm.debian.org/cgit/collab-maint/anthy.git
    - https://github.com/chewing/libchewing
    - https://github.com/choehwanjin/libhangul
    - https://github.com/rime/librime

* Implementations
    - https://github.com/choehwanjin/nabi
    - https://github.com/choehwanjin/imhangul
    - https://github.com/choehwanjin/ibus-hangul
    - https://github.com/ibus/ibus
    - https://github.com/fcitx/fcitx
    - https://github.com/fcitx/fcitx-qt5
    - https://github.com/uim/uim


# License

      Nimf is free software: you can redistribute it and/or modify it
      under the terms of the GNU Lesser General Public License as published
      by the Free Software Foundation, either version 3 of the License, or
      (at your option) any later version.

      Nimf is distributed in the hope that it will be useful, but
      WITHOUT ANY WARRANTY; without even the implied warranty of
      MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
      See the GNU Lesser General Public License for more details.

      You should have received a copy of the GNU Lesser General Public License
      along with this program;  If not, see <http://www.gnu.org/licenses/>.
