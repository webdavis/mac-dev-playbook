# KeePass Device Integration with Strongbox

[Strongbox](https://strongboxsafe.com/) is used to integrate KeePass databases across Mac and
iOS devices.

## Setup Instructions

1. Ensure Strongbox and [KeePassXC](https://keepassxc.org/) are installed on your Mac (this
   Ansible playbook should install them).

2. Move the KeePass database to the Strongbox iCloud folder at
   `~/Library/Mobile\ Documents/iCloud~com~strongbox/Documents/keepass.kdbx`. This will ensure
   that Strongbox can share databases across iOS and and Mac devices via iCloud.

3. On Mac, KeePassXC will be used to manage passwords, so just point it at the file path listed
   in the previous step. As long as the databases exist there then any changes made to the
   Database in KeePassXC will be synced across other Mac and iOS devices.
