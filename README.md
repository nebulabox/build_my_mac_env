Build My Mac Env
=======================================
This is a project that contains all the necessary configuration
files, scripts and instructions to build various open source apps
for Mac OS. This project uses [GNOME jhbuild](https://developer.gnome.org/jhbuild/).

General Instructions
---------------------------------------
1.	Bootstrap basic jhbuild and gtk environment.

2.	Build apps.

Bootstrap
---------------------------------------

Change `bootstrap-setup.sh` for the `jhbuild` source folder. The default install jhbuild in ~/Source and create ~/.local/bin/jhbuild. It will also install `~/.jhbuildrc` and `~/.jhbuildrc-custom` and will copy the current gtk-osx modules into `~/Source/jhbuild/modulesets`.

Run `sh bootstrap-setup.sh`

Edit `~/.jhbuildrc-custom`, append following lines to the end of file.

```
setup_release()
checkoutroot = "~/Source/src"
prefix = "/usr/local"
moduleset = os.path.expanduser('~') + "[xxx]/build_my_mac_env/modulesets/gtk-osx.modules"
use_local_modulesets = True
```

Run `jhbuild bootstrap`

Install curl (Optional)
---------------------------------------
```bash
jhbuild -m myapps.modules build curl
# or use system curl and don't check cert
echo insecure >> ~/.curlrc 
```

Install Python
---------------------------------------
```bash
jhbuild -m "gtk-osx-modulesets/gtk-osx.modules" build python
```

Install GTK-OSX Core ALL
---------------------------------------
```bash
jhbuild -m "modulesets/gtk-osx.modules" build meta-gtk-osx-bootstrap 
jhbuild -m "modulesets/gtk-osx.modules" build meta-gtk-osx-core  # gtk2
jhbuild -m "modulesets/gtk-osx.modules" build meta-gtk-osx-gtk3 # gtk3
jhbuild -m "modulesets/gtk-osx.modules" build meta-gtk-osx-themes meta-gtk-osx-gtk3-core-themes
jhbuild -m "modulesets/gtk-osx.modules" build meta-gtk-osx-python meta-gtk-osx-python-gtk3
jhbuild -m "modulesets/gtk-osx.modules" build meta-gtk-osx-gtkmm meta-gtk-osx-gtkmm3 
jhbuild -m "modulesets/gtk-osx.modules" build meta-gtk-osx-webkit meta-gtk-osx-webkit-gtk3
jhbuild -m "modulesets/gtk-osx.modules" build meta-gstreamer
```



