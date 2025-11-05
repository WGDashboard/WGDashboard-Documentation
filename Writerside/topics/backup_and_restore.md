# Backup and Restore

WGDashboard allows users/admins to backup and restore WireGuard configurations.<br>
This guide serves as a basic usage instruction.<br>

## Backing-up

The way we can make a backup is to navigate to:

1. Your targeted configuration
2. `Configuration Settings`
3. `Backup & Restore`

Then you will be presented with the main backup dialogue window.<br>
This window will be empty on first encounter (unless scripts or other tasks have acted).<br>

![main backup dialogue](../images/empty_backup.png)

To create a backup, simply click the button which says `Create Backup`.<br>
This will create copies of the current database contents and configuration file into: `/etc/wireguard/WGDashboard_Backup`.<br>

See:<br>

![single created backup](../images/single_backup.png)

Correlates to:<br>

```
wgdashboard:/etc/wireguard/WGDashboard_Backup# ls -l

total 8
-rw-------    1 root     root           493 Nov  5 16:11 wg0_20251105161129.conf
-rw-r--r--    1 root     root           488 Nov  5 16:11 wg0_20251105161129.sql
```

The download button which should be available on each created backup will download a .zip file with both files per configuration.<br>

## Restore

If you want to restore a backup from the files which have been obtained through the above method.<br>
Both from a different system and on the same system - the steps are the same.<br>
First off, extract a possible archive (zip, 7z, tar.gz) so you have the two standalone files (per configuration).<br>

Place them into the `/etc/wireguard/WGDashboard_Backup`.<br>
This should create a situation which is very similar to just having created a backup.<br>

Back in the Web-interface, check out the before-mentioned `Backup & Restore` tab again.<br>
You should see the that the files you have placed have created a dialogue - with a restore option.<br>
This restore option reverts the current configuration to the state inside the files.

See the video as an example:<br>

<img src="../images/example_restore.gif" alt="example restore video" width="950" height="425">

<toc></toc>