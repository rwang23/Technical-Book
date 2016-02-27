#SFTP Bash Command
###SFTP
	sftp rwang23@betaweb.csug.rochester.edu
	lpwd   Local working directory: /
	pwd    Remote working directory: /tecmint/
	ls     on remote
	lls    on local
	put    local.profile
	get     SettlementReport_1-10th.xls
	cd      on remote
	lcd     on local
	mkdir   on remote
	lmkdir  on local
	rm      on remote
	rmdir
	!
	exit    exit


##Options modify the behavior of commands:

	ls -a lists all contents of a directory, including hidden files and directories
	ls -l lists all contents in long format
	ls -t orders files and directories by the time they were last modified

###Multiple options can be used together, like ls -alt
From the command line, you can also copy, move, and remove files and directories:

	cp copies files
	mv moves and renames files
	rm removes files
	rm -r removes directories
Wildcards are useful for selecting groups of files and directories
