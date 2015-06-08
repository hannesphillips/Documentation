#Chmod System Call

Documentation on the 'chmod()' system call which is used to change the mode and/or permissions of a file.

##Chmod

##Inclusion

'#include <sys/types.h>'
'#include <sys/stat.h>'

##Declaration

'int chmod(const char *path, mode_t mode);'

##Return Value

Upon successful completion that the file has been changed, then a 0 is returned. Other wise -1 is returned and 'errno' is set to find the specific erro and no change to the file mode has occured.

##Description

chmod() is used to change S_ISUID, S_ISGID, S_ISVTX, and other file permission bits that have been named by a pathname, 'path', to the corresponding bits in the 'mode' parameter. 

The file permission bits that are changed are defined in 'sys/stat.h' 

1. S_ISUID - A set-user ID on an execute bit, on 04000 usually.
2. S_ISGID - Similar to S_ISUID but on 02000 usually. Takes a new file group from parent directory.
3. S_ISVTX - A sticky bit, usually 01000 that gives permission to delete a file in that directory only if the file is one that you own. If this is set to a non-directory file, the behavior will be unspecified. 
 
Many other permission bits can be used with this function, but it all varies on what specifically needs to be done. For example, setting read, write, exexecute permissions all have different permissions to be passed in. (S_IRUSR, S_IWUSR, S_IXUSR)

##Examples
'#include <sys/stat.h>

int main()
{
	const char *path;
	*/Insert code here/*

	chmod(path, S_IRUSR, S_IRGRP, S_IROTH);
}'

In the example listed above, we can see how chmod() can be used to change permissions for the user, group and others. This example sets read permissions for all.

However if you can see that the mode parameter has 3 different permissions that can be passed in. If you would like to only set read for the owner only,you only need to pass in S_IRUSR.

'#include <sys/stat.h> 

int main()
{
	const char *path;
	*/inser code here*/

	chmod(path, S_IRUSR);
}'

If read, write, and execute permissions for the owner only is what you would like to do, then it would be the same code listed above but with S_IRWXU passed in as 'mode'. 

You can find a list of permissions here depending on what you would need to change. Take the time to look through and see what specifically needs to be done!
'

[List of permissions](www.delorie.com/gnu/docs/glibc/libc_288.html)


