# Backup Script

## Usage:

	backup BACKUP_FOLDER
	backup -add FOLDER_TO_BACKUP

The backup script uses the rsync utility to maintain a backup of specified files in `BACKUP_FOLDER`. This list of files is maintained in `~/.backupinfo` and can be added to by using the `-add` option.

#### Example: Adding a file to ~/.backupinfo
`~/.backupinfo` maintains a list of **relative** paths (take note - paths are *relative*!) from your home folder (specified by `~` or `$HOME`) to various folders you want to backup. Suppose you want to backup all files in the directory `~/Documents/MyImportantDocuments`. This can be done by executing:
	
	backup -add Documents/MyImportantDocuments/**

Again, the relative (*not* the absolute!) path from your home directory must be specified. Unless you are familiar with the rsync utility, please do not manually edit `~/.backupinfo`, as the format and order of the file list is important and changing it may cause the script to fail.

#### Example: Backing up to a folder
If you want to backup to a folder, for example `"~/Google Drive/backup"`, simply run:

	backup "~/Google Drive/backup"

Note: the quotes are necessary if there is a space in the name (alternatively you can use `'\ '`). The script by default logs output to stdout. If you wish to create a log instead, simply redirect the output like so:

	backup "~/Google Drive/backup" > "~/Google Drive/backup/log.txt"

## Further Advice:
One excellent way of utilizing this script is by adding it to your crontab. The crontab executes the script at regular intervals which you can specify. To edit the crontab execute:

	crontab -e

This should open an editor, where you can add:

	MAILTO=''
	0 * * * * /<path to script>/backup BACKUP_FOLDER > BACKUP_FOLDER/log.txt

This will execute the script every hour. The `MAILTO=''` suppresses the mail sent by the cron daemon upon execution of the script.

For more information on rsync or crontab, see their man pages.


