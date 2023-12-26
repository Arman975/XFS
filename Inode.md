#Inode
In XFS, the traditional concept of an "Inode" found in other Unix file systems is replaced by the Extended Attribute Fork (EAF). 
The EAF serves as a metadata storage mechanism, containing crucial file attributes and other metadata associated with files.
XFS employs a B-Tree structure within the Extended Attribute Fork to organize and manage metadata efficiently across large file systems.

#Code 
# Open xfs_db in read-only mode for a specific device (replace /dev/sdX with your XFS device)
xfs_db -r /dev/sdX

# Use inode command to inspect a specific inode (replace <inode_number> with the actual inode number)
inode <inode_number>

# Quit xfs_db
quit

The xfs_db tool is invoked with the -r flag to open the XFS file system in read-only mode.
Upon opening xfs_db, the inode command is used to inspect a specific Inode by providing its inode number.
The specific inode number can be obtained through commands like ls -i or by other means.
The quit command is used to exit the xfs_db interface.


