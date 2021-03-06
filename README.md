# Neutrinet YunoHost App

This application is for Neutrinet members that have an Internet Cube configured has expected.

For now it does 2 things:

* fixed the situation where your certificate is outdated
* install neutrinet app list for YunoHost so you get updates for this app
* install labrique internet/internet cube app list for YunoHost so you get updates for this app

# Installation

Either put `https://github.com/neutrinet/neutrinet_ynh` in the administration interface at the bottom of the installation page or do this command in ssh:

    yunohost app install https://github.com/Neutrinet/neutrinet_ynh --verbose


# Known and "normal" warning/error messages during installation

If you see those, don't worry, it's not a bug.

After `+ sudo virtualenv ve --system-site-packages`

    Compiling /tmp/pip-build-0Vk8QK/pexpect/pexpect/async.py ...
      File "/tmp/pip-build-0Vk8QK/pexpect/pexpect/async.py", line 16
        transport, pw = yield from asyncio.get_event_loop()\
                                 ^
    SyntaxError: invalid syntax

This is due to the fact that we don't use python3 but python2 and that doesn't change anything here.

After `Running command 'yunohost app setting vpnclient login_passphrase -v "xxxxxxxxxxxxxxxxxxxxx"' ... done`

    Failed to open /dev/tty: No such device or address
    Failed to open /dev/tty: No such device or address
    Failed to open /dev/tty: No such device or address
    Failed to open /dev/tty: No such device or address
    Failed to open /dev/tty: No such device or address
    Failed to open /dev/tty: No such device or address
    Failed to open /dev/tty: No such device or address

It doesn't prevent the script from running.

# Publish a new version of the app

- edit the [upgrade](scripts/upgrade) script to bump the version
- update the `revision` with the current `sha` on the `master` branch, update the `lastUpdate` field in the [apps.json](https://neutrinet.be/apps.json) file
- test the updated version: 
  - check current version of the app on your cube: `yunohost app setting neutrinet version`
  - update the app with the latest version from master: `yunohost app upgrade neutrinet -u https://github.com/Neutrinet/neutrinet_ynh`
  - check the app has been updated: `yunohost app setting neutrinet version`
  - set the app to a previous version if you want to re-test the update: `yunohost app setting neutrinet version -v "0.2.2"`
