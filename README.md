# createinstalliso

```
createinstalliso <source>
```

**createinstalliso** creates an iso disk image from a macOS install application for use as an installation startup disk for virtual machines created with VMware, Parallels, Virtual Box or other virtualization software running on Mac hardware.

The **source** can be either a folder or a disk image.

If you specify a folder, it can be

* a macOS install application or
* any folder that has an install application or InstallESD.dmg<sup>[1](#footnote1)</sup> somewhere inside it

If you specify a disk image, it can be

* an InstallESD.dmg<sup>[1](#footnote1)</sup>,
* a disk image containing a pkg that installs the install application that contains the InstallESD.dmg, or
* a disk image that has an install application on it

If you specify a folder that contains more than one install application or InstallESD.dmg, the newest one will be used.


## Downloading a macOS install application

The install application for the latest version of macOS is available by searching for "macOS" in the Mac App Store. Older versions are available via the Purchased tab of the Mac App Store or via download links from the Apple support web site.

After downloading a macOS install application from the Mac App Store, it may open automatically to start the installation process. Quit the application without doing the installation.

In some cases, downloading a macOS install application from the Mac App Store will result in a smaller "stub" installer instead of the full installer. Specifically, the Contents/SharedSupport folder will be missing. This script does not support this type of install application. To get the full installer, make sure the version of macOS on which you are downloading it is up to date or use a newer version of macOS to download it.

Apple now distributes the installers for some older versions of macOS on a disk image containing an installer pkg which installs the install application to your Applications folder. It's not necessary to run this installer pkg; this script can mount the disk image and extract the needed files from it automatically.

Do not download macOS install applications from third-party web sites because they could contain malware.


## Examples

```
createinstalliso /Applications/"Install macOS Sierra.app"
```

Creates an iso from the InstallESD.dmg<sup>[1](#footnote1)</sup> in the Contents/SharedSupport folder of the specified install application.

```
createinstalliso /Applications/"Install macOS Sierra.app"/Contents/SharedSupport/InstallESD.dmg
```

Creates an iso from the specified InstallESD.dmg<sup>[1](#footnote1)</sup>.

```
createinstalliso /Applications
```

Creates an iso from the newest InstallESD.dmg<sup>[1](#footnote1)</sup> in the specified folder.

```
createinstalliso ~/Downloads/InstallOS.dmg
```

Mounts the disk image, extracts the install application from the newest pkg at the root of the volume, and creates an iso from the InstallESD.dmg<sup>[1](#footnote1)</sup> inside that application.


## Compatibility

**createinstalliso** is intended to run on as many different macOS versions as possible, to work with as many different macOS install application versions as possible, to create iso disk images of the smallest size, and to use as little time and temporary disk space while doing so as possible. It has been tested to work with the following install applications:

* Install Mac OS X Lion.app (10.7.5)
* Install OS X Mountain Lion.app (10.8.5)
* Install OS X Mavericks.app (10.9.5)
* Install OS X Yosemite.app (10.10.5)
* Install OS X El Capitan.app (10.11.6)
* Install macOS Sierra.app (10.12.6)

The iso files created from the following install applications don't seem to work:

* Install macOS High Sierra.app (10.13.6)
* Install macOS Mojave.app (10.14.6)
* Install macOS Catalina.app (10.15.5)

I need to investigate that.


## License

[MIT](LICENSE.md)


## Footnotes

<a name="footnote1"></a><sup>1</sup>
When creating an iso for macOS High Sierra or later, BaseSystem.dmg must be in the same folder as InstallESD.dmg.
