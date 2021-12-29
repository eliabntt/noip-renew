# Script to auto renew/confirm noip.com free hosts

[noip.com](https://www.noip.com/) free hosts expire every month.
This script auto clicks web pages to renew the hosts,
using Python/Selenium with Chrome headless mode.

- Platform: Debian/Ubuntu/Raspbian/Arch Linux, no GUI needed (tested on Debian 9.x/10.x/Arch Linux); python 3.6+
- Ver: 1.2
- Ref: [Technical explanation for the code (Chinese)](http://www.jianshu.com/p/3c8196175147)
- Updated: 29 December 2021
- Author: loblab
- Fork Mantainer: eliabntt
- Contributor: [IDemixI](https://www.github.com/IDemixI)

![noip.com hosts](https://raw.githubusercontent.com/loblab/noip-renew/master/screenshot.png)

## Usage

1. Clone this repository to the device you will be running it from. (`git clone https://github.com/eliabntt/noip-renew.git`)
2. Run setup.sh and set your noip.com account information,
3. Run noip-renew-USERNAME command.

As a suggestion, run `setup.sh root` to save everything as root. In the current version of the code the password is store "encrypted" in a file which would be readable by anyone that has access to the pc if you do not do so. Alternatively, create a specific user for this purpose.

Check confirmed records from multiple log files:

``` bash
grep -h Confirmed *.log | grep -v ": 0" | sort
```

## Usage with Docker (not yet tested)

For docker users, run the following:
```sh
my_username='add username here'
my_password='add password here'
my_host_num='add number of hosts here'
debug_lvl=2
docker build -t loblab/selenium:debian .
echo -e "$(crontab -l)"$'\n'"12  3  *  *  1,3,5  docker run --network host loblab/selenium:debian ${my_username} ${my_password} ${my_host_num} ${debug_lvl}" | crontab -
```

## Remarks

The script is not designed to renew/update the dynamic DNS records, though the latest version does have this ability if requested.
Check [noip.com documentation](https://www.noip.com/integrate) for that purpose.
Most wireless routers support noip.com. For more information, check [here](https://www.noip.com/support/knowledgebase/what-devices-support-no-ips-dynamic-dns-update-service/).
You can also check [DNS-O-Matic](https://dnsomatic.com/) to update multiple noip.com DNS records.

