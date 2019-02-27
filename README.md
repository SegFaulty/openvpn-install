
### Installation on Ubuntu 16.04

on a freshly installed ubuntu:

create a helper function to simple edit config files

    function configLine {
      local OLD_LINE_PATTERN=$1; shift
      local NEW_LINE=$1; shift
      local FILE=$1
      local NEW=$(echo "${NEW_LINE}" | sed 's/\//\\\//g')
      touch "${FILE}"
      sed -i '/'"${OLD_LINE_PATTERN}"'/{s/.*/'"${NEW}"'/;h};${x;/./{x;q100};x}' "${FILE}"
      if [[ $? -ne 100 ]] && [[ ${NEW_LINE} != '' ]]
      then
        echo "${NEW_LINE}" >> "${FILE}"
      fi
    }

secure sshd:

`configLine "Port ." "Port 222" /etc/ssh/sshd_config`

`configLine "PasswordAuthentication ." "PasswordAuthentication no" /etc/ssh/sshd_config`

`systemctl reload sshd`

download and start openVpn installer:

`wget https://raw.githubusercontent.com/SegFaulty/openvpn-install/master/openvpn-install.sh -O openvpn-install.sh && bash openvpn-install.sh`

Once it ends, you can run it again to add more users or remove some of them:

`bash openvpn-install.sh`


--------
###Origin Readme


## openvpn-install
OpenVPN [road warrior](http://en.wikipedia.org/wiki/Road_warrior_%28computing%29) installer for Debian, Ubuntu and CentOS.

This script will let you setup your own VPN server in no more than a minute, even if you haven't used OpenVPN before. It has been designed to be as unobtrusive and universal as possible.

### I want to run my own VPN but don't have a server for that
You can get a little VPS from just $1/month at [VirMach](https://billing.virmach.com/aff.php?aff=4109&url=billing.virmach.com/cart.php?gid=1).

### Donations

If you want to show your appreciation, you can donate via [PayPal](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=VBAYDL34Z7J6L) or [cryptocurrency](https://pastebin.com/raw/M2JJpQpC). Thanks!
