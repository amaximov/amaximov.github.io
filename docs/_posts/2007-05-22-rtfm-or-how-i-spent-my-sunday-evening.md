---
permalink: /2007/5/22/rtfm-or-how-i-spent-my-sunday-evening
date: '2007-05-22 01:27:00'
title: >-
    rtfm or how i spent my sunday evening
---

dreading the impending move (or rather using it as an excuse to perform
many long-overdue housekeeping tasks), i have been virtualizing various
OS'es around the house (note how conveniently that eclipsed tasks like
getting rid of old furniture or boxing things up - truly, one is always
tempted to view everything to a technical problem).

first of all, note that there is a handy dandy jolly tool from vmware:
[vmware
converter](http://www.vmware.com/products/converter/ "vmware converter");
it will happily virtualize your windows machine (no more screwing around
with ghost/acronis/dd, like i used to).

![joy](/assets/2007/8/27/joyous_jogging.jpg)

still, i had a gentoo server confined within a wheezing old machine that
absolutely had to stay up (so no cold restores). casting a nostalgic
glance in the direction of dd/netcat combo, i opted for partimage and
[SysRescCD](http://www.sysresccd.org/ "SysRescCD"), but before that - `dd
if=/dev/hda of=hda-mbr-full bs=512 count=1` to save mbr; and to restore:
`dd if=hda-mbr-full of=/dev/hda bs=512 count=1`; then `sfdisk -d \> file`
then `sfdisk \< file` (nifty! i did not know that). boot from the rescue
cd, create partitions, restore `partimage` droppings (had to do it several
times, apparently it is no smarter than `dd` - no checksums!), `mkswap`,
etc, etc.

so far so good, but the main reason for this post is the mysterious
`vmware-modules` - i tried emergeing them, tried downloading them, read up
on forums, installed client api/sdk available from the download sites,
even read the docs! basically, being a [gentoo
user](http://web.archive.org/web/20060513022941/http://www.funroll-loops.org/),
i did not have generic drivers for my network card; once transplanted to
vmware, the OS refused to acknowledge network hardware. `vmware-modules`
were referred to as the ultimate answer.

finally, somewhere in the depths of google cache i found the answer -
drop-down VM menu, then select "Install VMWare tools..." followed by
`mount /dev/cdrom /mnt/tmp` gives you the ultimate joy - a `vmware-tools`
tarball. man, how is that not obvious?!! under windows this runs an
installer, but under linux it quietly slips in an iso under the guise of
`/dev/cdrom`

now it's just typing and [joyous
cargo-culting](http://en.wikipedia.org/wiki/Cargo_cult_software_engineering):

run the installer script, build the kernel modules, check'em with
`lsmod`, `symlink net.eth0` to network (boy, do i feel dirty), play some
more tricks to appease the gentoo startup script gods and vmware
reliance on redhat-like `rc`, and voila - vmware starts before `net\*`, `eth0`
pops up in `ifconfig` after you tweaked `/etc/conf.d/net`, (do not forget to
go under `Host -> Virtual Network Settings -> Automatic Bridging` and add
all the crap like VPN pseudo-adapters, otherwise it will get you, like
it gets me every time; then set `vmnet0` as the auto-bridged interface to
be used for vm).

phew! now i pick up a bottle of red and promptly forget all this
nonsense.
