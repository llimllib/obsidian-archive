here's the log of the installation script, I appreciate its thoroughness and clarity with what it's doing.

```console
$ sh <(curl -L https://nixos.org/nix/install)
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
100  4064  100  4064    0     0  11801      0 --:--:-- --:--:-- --:--:-- 11801
downloading Nix 2.10.3 binary tarball for aarch64-darwin from 'https://releases.nixos.org/nix/nix-2.10.3/nix-2.10.3-aarch64-darwin.tar.xz' to '/var/folders/cj/3fpctnd52vv37y9gpdgg7c200000gn/T/nix-binary-tarball-unpack.XXXXXXXXXX.MuRQXaVR'...
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 10.0M  100 10.0M    0     0  4336k      0  0:00:02  0:00:02 --:--:-- 4347k
Switching to the Multi-user Installer
Welcome to the Multi-User Nix Installation

This installation tool will set up your computer with the Nix package
manager. This will happen in a few stages:

1. Make sure your computer doesn't already have Nix. If it does, I
   will show you instructions on how to clean up your old install.

2. Show you what I am going to install and where. Then I will ask
   if you are ready to continue.

3. Create the system users and groups that the Nix daemon uses to run
   builds.

4. Perform the basic installation of the Nix files daemon.

5. Configure your shell to import special Nix Profile files, so you
   can use Nix.

6. Start the Nix daemon.

Would you like to see a more detailed list of what I will do?
[y/n] y


I will:

 - make sure your computer doesn't already have Nix files
   (if it does, I will tell you how to clean them up.)
 - create local users (see the list above for the users I'll make)
 - create a local group (nixbld)
 - install Nix in to /nix
 - create a configuration file in /etc/nix
 - set up the "default profile" by creating some Nix-related files in
   /var/root
 - back up /etc/bashrc to /etc/bashrc.backup-before-nix
 - update /etc/bashrc to include some Nix configuration
 - back up /etc/zshrc to /etc/zshrc.backup-before-nix
 - update /etc/zshrc to include some Nix configuration
 - create a Nix volume and a LaunchDaemon to mount it
 - create a LaunchDaemon (at /Library/LaunchDaemons/org.nixos.nix-daemon.plist) for nix-daemon

Ready to continue?
[y/n] y


---- let's talk about sudo -----------------------------------------------------
This script is going to call sudo a lot. Every time I do, it'll
output exactly what it'll do, and why.

Just like this:

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo echo

to demonstrate how our sudo prompts look


This might look scary, but everything can be undone by running just a
few commands. I used to ask you to confirm each time sudo ran, but it
was too many times. Instead, I'll just ask you this one time:

Can I use sudo?
[y/n] y

Yay! Thanks! Let's get going!

~~> Fixing any leftover Nix volume state
Before I try to install, I'll check for any existing Nix volume config
and ask for your permission to remove it (so that the installer can
start fresh). I'll also ask for permission to fix any issues I spot.

~~> Checking for artifacts of previous installs
Before I try to install, I'll check for signs Nix already is or has
been installed on this system.

---- Nix config report ---------------------------------------------------------
        Temp Dir:	/var/folders/cj/3fpctnd52vv37y9gpdgg7c200000gn/T/tmp.vw9LMP25sm
        Nix Root:	/nix
     Build Users:	32
  Build Group ID:	30000
Build Group Name:	nixbld

build users:
    Username:	UID
     _nixbld1:	301
     _nixbld2:	302
     _nixbld3:	303
     _nixbld4:	304
     _nixbld5:	305
     _nixbld6:	306
     _nixbld7:	307
     _nixbld8:	308
     _nixbld9:	309
     _nixbld10:	310
     _nixbld11:	311
     _nixbld12:	312
     _nixbld13:	313
     _nixbld14:	314
     _nixbld15:	315
     _nixbld16:	316
     _nixbld17:	317
     _nixbld18:	318
     _nixbld19:	319
     _nixbld20:	320
     _nixbld21:	321
     _nixbld22:	322
     _nixbld23:	323
     _nixbld24:	324
     _nixbld25:	325
     _nixbld26:	326
     _nixbld27:	327
     _nixbld28:	328
     _nixbld29:	329
     _nixbld30:	330
     _nixbld31:	331
     _nixbld32:	332

Ready to continue?
[y/n] y


---- Preparing a Nix volume ----------------------------------------------------
    Nix traditionally stores its data in the root directory /nix, but
    macOS now (starting in 10.15 Catalina) has a read-only root directory.
    To support Nix, I will create a volume and configure macOS to mount it
    at /nix.

~~> Configuring /etc/synthetic.conf to make a mount-point at /nix

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/ex -u NONE -n /etc/synthetic.conf

to add Nix to /etc/synthetic.conf

Password:

~~> Creating a Nix volume

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/diskutil apfs addVolume disk3 APFS Nix Store -nomount

to create a new APFS volume 'Nix Store' on disk3


---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/diskutil unmount force disk3s7

to ensure the Nix volume is not mounted

disk3s7 was already unmounted

~~> Configuring /etc/fstab to specify volume mount options

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/vifs

to add nix to fstab


~~> Encrypt the Nix volume

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/diskutil mount Nix Store

to mount your Nix volume for encrypting

Volume Nix Store on Nix Store mounted

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/security -i

to add your Nix volume's password to Keychain


---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/diskutil apfs encryptVolume Nix Store -user disk -stdinpassphrase

to actually encrypt your Nix volume

Encrypting with the new "Disk" crypto user on disk3s7
The new "Disk" user will be the only one who has initial access to disk3s7
The new APFS crypto user UUID will be 97380E24-A77F-4428-8811-F9F52FAFE024
Encryption has likely completed due to AES hardware; see "diskutil apfs list"

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/diskutil unmount force Nix Store

to unmount the encrypted volume

Volume Nix Store on disk3s7 force-unmounted

~~> Configuring LaunchDaemon to mount 'Nix Store'

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/ex -u NONE -n /Library/LaunchDaemons/org.nixos.darwin-store.plist

to install the Nix volume mounter


---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo launchctl bootstrap system /Library/LaunchDaemons/org.nixos.darwin-store.plist

to launch the Nix volume mounter


---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo launchctl kickstart -k system/org.nixos.darwin-store

to launch the Nix volume mounter


~~> Setting up the build group nixbld

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o create -r Nix build group for nix-daemon -i 30000 nixbld

Create the Nix build group, nixbld

            Created:	Yes

~~> Setting up the build user _nixbld1

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld1 UniqueID 301

Creating the Nix build user (#1), _nixbld1

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld1 IsHidden 1

in order to make _nixbld1 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld1 NFSHomeDirectory /var/empty

in order to give _nixbld1 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 1

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld1 UserShell /sbin/nologin

in order to give _nixbld1 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld1 nixbld

Add _nixbld1 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld1 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld2

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld2 UniqueID 302

Creating the Nix build user (#2), _nixbld2

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld2 IsHidden 1

in order to make _nixbld2 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld2 NFSHomeDirectory /var/empty

in order to give _nixbld2 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 2

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld2 UserShell /sbin/nologin

in order to give _nixbld2 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld2 nixbld

Add _nixbld2 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld2 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld3

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld3 UniqueID 303

Creating the Nix build user (#3), _nixbld3

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld3 IsHidden 1

in order to make _nixbld3 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld3 NFSHomeDirectory /var/empty

in order to give _nixbld3 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 3

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld3 UserShell /sbin/nologin

in order to give _nixbld3 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld3 nixbld

Add _nixbld3 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld3 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld4

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld4 UniqueID 304

Creating the Nix build user (#4), _nixbld4

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld4 IsHidden 1

in order to make _nixbld4 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld4 NFSHomeDirectory /var/empty

in order to give _nixbld4 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 4

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld4 UserShell /sbin/nologin

in order to give _nixbld4 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld4 nixbld

Add _nixbld4 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld4 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld5

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld5 UniqueID 305

Creating the Nix build user (#5), _nixbld5

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld5 IsHidden 1

in order to make _nixbld5 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld5 NFSHomeDirectory /var/empty

in order to give _nixbld5 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 5

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld5 UserShell /sbin/nologin

in order to give _nixbld5 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld5 nixbld

Add _nixbld5 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld5 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld6

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld6 UniqueID 306

Creating the Nix build user (#6), _nixbld6

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld6 IsHidden 1

in order to make _nixbld6 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld6 NFSHomeDirectory /var/empty

in order to give _nixbld6 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 6

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld6 UserShell /sbin/nologin

in order to give _nixbld6 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld6 nixbld

Add _nixbld6 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld6 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld7

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld7 UniqueID 307

Creating the Nix build user (#7), _nixbld7

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld7 IsHidden 1

in order to make _nixbld7 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld7 NFSHomeDirectory /var/empty

in order to give _nixbld7 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 7

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld7 UserShell /sbin/nologin

in order to give _nixbld7 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld7 nixbld

Add _nixbld7 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld7 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld8

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld8 UniqueID 308

Creating the Nix build user (#8), _nixbld8

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld8 IsHidden 1

in order to make _nixbld8 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld8 NFSHomeDirectory /var/empty

in order to give _nixbld8 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 8

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld8 UserShell /sbin/nologin

in order to give _nixbld8 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld8 nixbld

Add _nixbld8 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld8 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld9

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld9 UniqueID 309

Creating the Nix build user (#9), _nixbld9

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld9 IsHidden 1

in order to make _nixbld9 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld9 NFSHomeDirectory /var/empty

in order to give _nixbld9 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 9

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld9 UserShell /sbin/nologin

in order to give _nixbld9 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld9 nixbld

Add _nixbld9 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld9 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld10

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld10 UniqueID 310

Creating the Nix build user (#10), _nixbld10

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld10 IsHidden 1

in order to make _nixbld10 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld10 NFSHomeDirectory /var/empty

in order to give _nixbld10 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 10

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld10 UserShell /sbin/nologin

in order to give _nixbld10 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld10 nixbld

Add _nixbld10 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld10 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld11

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld11 UniqueID 311

Creating the Nix build user (#11), _nixbld11

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld11 IsHidden 1

in order to make _nixbld11 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld11 NFSHomeDirectory /var/empty

in order to give _nixbld11 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 11

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld11 UserShell /sbin/nologin

in order to give _nixbld11 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld11 nixbld

Add _nixbld11 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld11 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld12

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld12 UniqueID 312

Creating the Nix build user (#12), _nixbld12

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld12 IsHidden 1

in order to make _nixbld12 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld12 NFSHomeDirectory /var/empty

in order to give _nixbld12 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 12

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld12 UserShell /sbin/nologin

in order to give _nixbld12 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld12 nixbld

Add _nixbld12 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld12 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld13

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld13 UniqueID 313

Creating the Nix build user (#13), _nixbld13

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld13 IsHidden 1

in order to make _nixbld13 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld13 NFSHomeDirectory /var/empty

in order to give _nixbld13 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 13

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld13 UserShell /sbin/nologin

in order to give _nixbld13 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld13 nixbld

Add _nixbld13 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld13 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld14

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld14 UniqueID 314

Creating the Nix build user (#14), _nixbld14

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld14 IsHidden 1

in order to make _nixbld14 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld14 NFSHomeDirectory /var/empty

in order to give _nixbld14 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 14

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld14 UserShell /sbin/nologin

in order to give _nixbld14 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld14 nixbld

Add _nixbld14 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld14 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld15

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld15 UniqueID 315

Creating the Nix build user (#15), _nixbld15

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld15 IsHidden 1

in order to make _nixbld15 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld15 NFSHomeDirectory /var/empty

in order to give _nixbld15 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 15

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld15 UserShell /sbin/nologin

in order to give _nixbld15 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld15 nixbld

Add _nixbld15 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld15 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld16

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld16 UniqueID 316

Creating the Nix build user (#16), _nixbld16

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld16 IsHidden 1

in order to make _nixbld16 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld16 NFSHomeDirectory /var/empty

in order to give _nixbld16 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 16

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld16 UserShell /sbin/nologin

in order to give _nixbld16 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld16 nixbld

Add _nixbld16 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld16 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld17

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld17 UniqueID 317

Creating the Nix build user (#17), _nixbld17

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld17 IsHidden 1

in order to make _nixbld17 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld17 NFSHomeDirectory /var/empty

in order to give _nixbld17 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 17

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld17 UserShell /sbin/nologin

in order to give _nixbld17 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld17 nixbld

Add _nixbld17 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld17 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld18

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld18 UniqueID 318

Creating the Nix build user (#18), _nixbld18

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld18 IsHidden 1

in order to make _nixbld18 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld18 NFSHomeDirectory /var/empty

in order to give _nixbld18 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 18

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld18 UserShell /sbin/nologin

in order to give _nixbld18 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld18 nixbld

Add _nixbld18 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld18 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld19

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld19 UniqueID 319

Creating the Nix build user (#19), _nixbld19

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld19 IsHidden 1

in order to make _nixbld19 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld19 NFSHomeDirectory /var/empty

in order to give _nixbld19 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 19

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld19 UserShell /sbin/nologin

in order to give _nixbld19 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld19 nixbld

Add _nixbld19 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld19 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld20

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld20 UniqueID 320

Creating the Nix build user (#20), _nixbld20

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld20 IsHidden 1

in order to make _nixbld20 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld20 NFSHomeDirectory /var/empty

in order to give _nixbld20 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 20

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld20 UserShell /sbin/nologin

in order to give _nixbld20 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld20 nixbld

Add _nixbld20 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld20 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld21

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld21 UniqueID 321

Creating the Nix build user (#21), _nixbld21

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld21 IsHidden 1

in order to make _nixbld21 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld21 NFSHomeDirectory /var/empty

in order to give _nixbld21 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 21

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld21 UserShell /sbin/nologin

in order to give _nixbld21 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld21 nixbld

Add _nixbld21 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld21 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld22

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld22 UniqueID 322

Creating the Nix build user (#22), _nixbld22

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld22 IsHidden 1

in order to make _nixbld22 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld22 NFSHomeDirectory /var/empty

in order to give _nixbld22 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 22

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld22 UserShell /sbin/nologin

in order to give _nixbld22 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld22 nixbld

Add _nixbld22 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld22 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld23

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld23 UniqueID 323

Creating the Nix build user (#23), _nixbld23

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld23 IsHidden 1

in order to make _nixbld23 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld23 NFSHomeDirectory /var/empty

in order to give _nixbld23 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 23

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld23 UserShell /sbin/nologin

in order to give _nixbld23 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld23 nixbld

Add _nixbld23 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld23 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld24

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld24 UniqueID 324

Creating the Nix build user (#24), _nixbld24

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld24 IsHidden 1

in order to make _nixbld24 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld24 NFSHomeDirectory /var/empty

in order to give _nixbld24 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 24

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld24 UserShell /sbin/nologin

in order to give _nixbld24 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld24 nixbld

Add _nixbld24 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld24 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld25

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld25 UniqueID 325

Creating the Nix build user (#25), _nixbld25

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld25 IsHidden 1

in order to make _nixbld25 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld25 NFSHomeDirectory /var/empty

in order to give _nixbld25 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 25

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld25 UserShell /sbin/nologin

in order to give _nixbld25 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld25 nixbld

Add _nixbld25 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld25 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld26

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld26 UniqueID 326

Creating the Nix build user (#26), _nixbld26

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld26 IsHidden 1

in order to make _nixbld26 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld26 NFSHomeDirectory /var/empty

in order to give _nixbld26 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 26

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld26 UserShell /sbin/nologin

in order to give _nixbld26 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld26 nixbld

Add _nixbld26 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld26 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld27

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld27 UniqueID 327

Creating the Nix build user (#27), _nixbld27

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld27 IsHidden 1

in order to make _nixbld27 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld27 NFSHomeDirectory /var/empty

in order to give _nixbld27 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 27

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld27 UserShell /sbin/nologin

in order to give _nixbld27 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld27 nixbld

Add _nixbld27 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld27 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld28

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld28 UniqueID 328

Creating the Nix build user (#28), _nixbld28

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld28 IsHidden 1

in order to make _nixbld28 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld28 NFSHomeDirectory /var/empty

in order to give _nixbld28 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 28

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld28 UserShell /sbin/nologin

in order to give _nixbld28 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld28 nixbld

Add _nixbld28 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld28 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld29

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld29 UniqueID 329

Creating the Nix build user (#29), _nixbld29

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld29 IsHidden 1

in order to make _nixbld29 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld29 NFSHomeDirectory /var/empty

in order to give _nixbld29 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 29

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld29 UserShell /sbin/nologin

in order to give _nixbld29 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld29 nixbld

Add _nixbld29 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld29 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld30

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld30 UniqueID 330

Creating the Nix build user (#30), _nixbld30

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld30 IsHidden 1

in order to make _nixbld30 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld30 NFSHomeDirectory /var/empty

in order to give _nixbld30 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 30

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld30 UserShell /sbin/nologin

in order to give _nixbld30 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld30 nixbld

Add _nixbld30 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld30 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld31

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld31 UniqueID 331

Creating the Nix build user (#31), _nixbld31

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld31 IsHidden 1

in order to make _nixbld31 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld31 NFSHomeDirectory /var/empty

in order to give _nixbld31 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 31

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld31 UserShell /sbin/nologin

in order to give _nixbld31 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld31 nixbld

Add _nixbld31 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld31 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the build user _nixbld32

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . create /Users/_nixbld32 UniqueID 332

Creating the Nix build user (#32), _nixbld32

           Created:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld32 IsHidden 1

in order to make _nixbld32 a hidden user

            Hidden:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld32 NFSHomeDirectory /var/empty

in order to give _nixbld32 a safe home directory

    Home Directory:	/var/empty
              Note:	Nix build user 32

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld32 UserShell /sbin/nologin

in order to give _nixbld32 a safe home directory

   Logins Disabled:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/dseditgroup -o edit -t user -a _nixbld32 nixbld

Add _nixbld32 to the nixbld group

  Member of nixbld:	Yes

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/bin/dscl . -create /Users/_nixbld32 PrimaryGroupID 30000

to let the nix daemon use this user for builds (this might seem redundant, but there are two concepts of group membership)

    PrimaryGroupID:	30000

~~> Setting up the basic directory structure

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /usr/sbin/chown -R root:nixbld /nix

to take root ownership of existing Nix store files


---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo install -dv -m 0755 /nix /nix/var /nix/var/log /nix/var/log/nix /nix/var/log/nix/drvs /nix/var/nix /nix/var/nix/db /nix/var/nix/gcroots /nix/var/nix/profiles /nix/var/nix/temproots /nix/var/nix/userpool /nix/var/nix/daemon-socket /nix/var/nix/gcroots/per-user /nix/var/nix/profiles/per-user

to make the basic directory structure of Nix (part 1)

install: mkdir /nix/var
install: mkdir /nix/var/log
install: mkdir /nix/var/log/nix
install: mkdir /nix/var/log/nix/drvs
install: mkdir /nix/var/nix
install: mkdir /nix/var/nix/db
install: mkdir /nix/var/nix/gcroots
install: mkdir /nix/var/nix/profiles
install: mkdir /nix/var/nix/temproots
install: mkdir /nix/var/nix/userpool
install: mkdir /nix/var/nix/daemon-socket
install: mkdir /nix/var/nix/gcroots/per-user
install: mkdir /nix/var/nix/profiles/per-user

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo install -dv -g nixbld -m 1775 /nix/store

to make the basic directory structure of Nix (part 2)

install: mkdir /nix/store

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo install -dv -m 0555 /etc/nix

to place the default nix daemon configuration (part 1)

install: mkdir /etc/nix

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo install -m 0664 /var/folders/cj/3fpctnd52vv37y9gpdgg7c200000gn/T/tmp.vw9LMP25sm/.nix-channels /var/root/.nix-channels

to set up the default system channel (part 1)


~~> Installing Nix

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo cp -RPp ./store/0ky7rhm0ckf4vw7vg2v5cyarrbsblvmj-aws-crt-cpp-0.17.28 ./store/1dcbaii28xnv98zw2w5f0skn2mar1ck8-aws-c-auth-0.6.13 ./store/2033pdgsv4wgl0zx6nng9i8q5f4h18lk-libidn2-2.3.2 ./store/2im4pw4pl5zsr6mjhwrjfcinrl9qljhy-nss-cacert-3.80 ./store/3b8r3yspv7f7p92jfxg548cfxi7q19d7-bash-5.1-p16 ./store/3k2ygb7mk9ylm2r5g0iad7akg1qwas4g-libssh2-1.10.0 ./store/3qcn93slgnm0wz74fq3nsd2942k3vsfm-aws-c-cal-0.5.17 ./store/58ppyba9pbc8yxqiw11gv9aw2adh1lgg-libxml2-2.9.14 ./store/6d17z21w7h8vmpsnmr8dm73sb3mvkpp0-nlohmann_json-3.10.5 ./store/789cl5k5ca0m9sxkiqyl4ackv5f0cmfz-aws-sdk-cpp-1.9.238 ./store/79z2m5vwbqwzrmfsbbv6rvk04z2nzf0x-curl-7.83.1 ./store/7hn69mlypdg285ar3ia71prgcrsx521g-libiconv-50 ./store/7m37v9mnii266p2l21xl97s4666f7d2s-libarchive-3.6.1-lib ./store/7vfyla60szbi8h35q93mrsij6whb3q9q-aws-c-compression-0.2.14 ./store/8yr5vy7jasrizvnvm9d12iynbbvf8r3p-nghttp2-1.47.0-lib ./store/962rka435k9c9p5ng1z2y3gspi4gs7hr-libcxxabi-11.1.0 ./store/9h5pks3l96gkp7653x4jxsfz1ca41fdc-aws-c-io-0.11.0 ./store/9jzvhm113w1xndcc5p4lvbqpqvk01c17-aws-c-mqtt-0.7.10 ./store/9x2z66kf8g8p9y1bxkraspghsy8jb5nj-zstd-1.5.2 ./store/a08j7vsgfcvzx0ahl986v38mjrx3gkm0-brotli-1.0.9-lib ./store/blnw8pnh6srwwr31g23mh6b70g6viaam-libcxx-11.1.0 ./store/cfc8xcp3q1ccx9wrfkbagia95w6rsvsh-apple-framework-Security-11.0.0 ./store/cpl9nndqjgn238p3kdwws845gscavfh4-sqlite-3.38.5 ./store/czwp4nmcn5skjiylhbyhg5k21wv76w9j-libsodium-1.0.18 ./store/d1hxdg09lxql958cmnrjq68alnd73i39-aws-c-s3-0.1.39 ./store/dg4r67wwna6sb2drh7gj38byq91ix2z9-aws-c-common-0.7.0 ./store/gp7k17iy1n7hgf97qwnxw28c6v9nhb1i-nix-2.10.3 ./store/gwxhwcf0m9yrhz5wql1181bjfp654m1b-zlib-1.2.12 ./store/h9z5lncphgm9if86wxrfqg7w7fv7khbh-libkrb5-1.19.3 ./store/jgwmpgiin89dp0jjpjlwily6fgj1xs1a-aws-c-sdkutils-0.1.2 ./store/kd48xgjihd6sz5gvf2bvj7kw7m7ybhmf-xz-5.2.5 ./store/n2bygl2nqg7r35mg4ny45cwkarxgx2xb-curl-7.83.1 ./store/nf20p297fz6sfs97m7rl7al9ywchi83n-openssl-1.1.1q ./store/p7755cvgiwvv6lvin1r25jy711p8fn2n-libunistring-1.0 ./store/r6y0rvzx8z9z459ghmj1zrnpi4r7xa5v-aws-checksums-0.1.12 ./store/s5ikc3jlv67j9bm8463rjz3x09lcwm8v-aws-c-http-0.6.15 ./store/v2p3injpwnyf31vfllpz2k172mr58fn9-apple-lib-libDER ./store/vzbnm6afkdcbgb57npl06gk7rsap4sfy-apple-framework-CoreFoundation-11.0.0 ./store/w18g47jdi000hq064cb83j42kmbc4k3s-editline-1.17.1 ./store/w5n081lpdyhc5aa69cq59j9s1h626jgj-apple-framework-IOKit-11.0.0 ./store/xi7bwrkki4fwr6zam7gmcklnqq3f3d5h-aws-c-event-stream-0.2.7 ./store/y9j96x0zkxwwbqknr66r7bwczlxa4kk6-bzip2-1.0.6.0.2 ./store/y9rzzima6wdy0ph29ff09hr8vadfkx16-libobjc-11.0.0 ./store/z1l79b1phxy2yzcwsvn0ar121gcnh0x6-boehm-gc-8.0.6 /nix/store/

to copy the basic Nix files to the new store at /nix/store


---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo chmod -R ugo-w /nix/store/

to make the new store non-writable at /nix/store

      Alright! We have our first nix at /nix/store/gp7k17iy1n7hgf97qwnxw28c6v9nhb1i-nix-2.10.3

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /nix/store/gp7k17iy1n7hgf97qwnxw28c6v9nhb1i-nix-2.10.3/bin/nix-store --load-db

to load data for the first time in to the Nix Database

warning: $HOME ('/Users/llimllib') is not owned by you, falling back to the one defined in the 'passwd' file
      Just finished getting the nix database ready.

~~> Setting up shell profiles: /etc/bashrc /etc/profile.d/nix.sh /etc/zshrc /etc/bash.bashrc /etc/zsh/zshrc

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo cp /etc/bashrc /etc/bashrc.backup-before-nix

to back up your current /etc/bashrc to /etc/bashrc.backup-before-nix


---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo tee -a /etc/bashrc

extend your /etc/bashrc with nix-daemon settings


# Nix
if [ -e '/nix/var/nix/profiles/default/etc/profile.d/nix-daemon.sh' ]; then
  . '/nix/var/nix/profiles/default/etc/profile.d/nix-daemon.sh'
fi
# End Nix


---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo cp /etc/zshrc /etc/zshrc.backup-before-nix

to back up your current /etc/zshrc to /etc/zshrc.backup-before-nix


---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo tee -a /etc/zshrc

extend your /etc/zshrc with nix-daemon settings


# Nix
if [ -e '/nix/var/nix/profiles/default/etc/profile.d/nix-daemon.sh' ]; then
  . '/nix/var/nix/profiles/default/etc/profile.d/nix-daemon.sh'
fi
# End Nix


---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo touch /etc/bash.bashrc

to create a stub /etc/bash.bashrc which will be updated


---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo tee -a /etc/bash.bashrc

extend your /etc/bash.bashrc with nix-daemon settings


# Nix
if [ -e '/nix/var/nix/profiles/default/etc/profile.d/nix-daemon.sh' ]; then
  . '/nix/var/nix/profiles/default/etc/profile.d/nix-daemon.sh'
fi
# End Nix


~~> Setting up the default profile

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo HOME=/var/root /nix/store/gp7k17iy1n7hgf97qwnxw28c6v9nhb1i-nix-2.10.3/bin/nix-env -i /nix/store/gp7k17iy1n7hgf97qwnxw28c6v9nhb1i-nix-2.10.3

to install a bootstrapping Nix in to the default profile

installing 'nix-2.10.3'
building '/nix/store/p0k45jgawx7xdvfpp2q52an0dwq9idx1-user-environment.drv'...

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo HOME=/var/root /nix/store/gp7k17iy1n7hgf97qwnxw28c6v9nhb1i-nix-2.10.3/bin/nix-env -i /nix/store/2im4pw4pl5zsr6mjhwrjfcinrl9qljhy-nss-cacert-3.80

to install a bootstrapping SSL certificate just for Nix in to the default profile

installing 'nss-cacert-3.80'
building '/nix/store/dlc7sx0vzcwyp337cmw9dndrjs8g6hnc-user-environment.drv'...

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo HOME=/var/root NIX_SSL_CERT_FILE=/nix/var/nix/profiles/default/etc/ssl/certs/ca-bundle.crt /nix/store/gp7k17iy1n7hgf97qwnxw28c6v9nhb1i-nix-2.10.3/bin/nix-channel --update nixpkgs

to update the default channel in the default profile

unpacking channels...

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo install -m 0664 /var/folders/cj/3fpctnd52vv37y9gpdgg7c200000gn/T/tmp.vw9LMP25sm/nix.conf /etc/nix/nix.conf

to place the default nix daemon configuration (part 2)


~~> Setting up the nix-daemon LaunchDaemon

---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo /bin/cp -f /nix/var/nix/profiles/default/Library/LaunchDaemons/org.nixos.nix-daemon.plist /Library/LaunchDaemons/org.nixos.nix-daemon.plist

to set up the nix-daemon as a LaunchDaemon


---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo launchctl load /Library/LaunchDaemons/org.nixos.nix-daemon.plist

to load the LaunchDaemon plist for nix-daemon


---- sudo execution ------------------------------------------------------------
I am executing:

    $ sudo launchctl kickstart -k system/org.nixos.nix-daemon

to start the nix-daemon

Alright! We're done!
Try it! Open a new terminal, and type:

  $ nix-shell -p nix-info --run "nix-info -m"

Thank you for using this installer. If you have any feedback or need
help, don't hesitate:

You can open an issue at https://github.com/nixos/nix/issues

Or feel free to contact the team:
 - Matrix: #nix:nixos.org
 - IRC: in #nixos on irc.libera.chat
 - twitter: @nixos_org
 - forum: https://discourse.nixos.org

---- Reminders -----------------------------------------------------------------
[ 1 ]
Nix won't work in active shell sessions until you restart them.
```