My steps to make a Slackware container running with [LXC Plugin](https://github.com/ich777/unraid-lxc-plugin) on Unraid

---

I got the initial file from https://slackware.uk/slackware/slackware64-15.0/source/ap/lxc/lxc-slackware.in

See the [commit history](https://github.com/fabricionaweb/lxc-slackware/commits/main/usr/share/lxc/templates/lxc-slackware) to understand the changes I have done.

### Prepare

1. To compile the template, you need to first install two packages on Unraid host:

   - slackpkg

     ```sh
     wget https://slackware.uk/slackware/slackware64-15.0/slackware64/ap/slackpkg-15.0.10-noarch-1.txz
     installpkg slackpkg-*
     ```

   - gnupg (v1)

     ```sh
     wget https://slackware.uk/slackware/slackware64-15.0/slackware64/n/gnupg-1.4.23-x86_64-4.txz
     installpkg gnupg-*
     ```

   > **Warning**
   > This packages will not persist after reboot.

2. Download the template to the right place and give permissions:

   ```sh
   wget -P /usr/share/lxc/templates https://raw.githubusercontent.com/fabricionaweb/lxc-slackware/main/usr/share/lxc/templates/lxc-slackware
   chmod 755 /usr/share/lxc/templates/lxc-slackware
   ```

   _755 is the same as the others_

   > **Warning**
   > This file will not persist after reboot.

### Create

After that, assuming you have the [LXC Plugin](https://github.com/ich777/unraid-lxc-plugin) installed, you just create the container manually

```sh
lxc-create --name my-slackware-container --template slackware -- --release 15.0
```
