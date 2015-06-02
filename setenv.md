#Setenv System Call


This file will include information pertaining to 'setenv'. 


##setenv:

[man page](http://linux.die.net/man/3/setenv)

To use this system call make sure to include the following library

``#include <stdlib.h>``

The paramaters are as follows:

``int setenv(const char *name, const char *value, int overwrite);``

``int unsetenv(const char *name);``

#####Description
The main purpose of the `setenv()` system call is to change the name based on the value that is passed in, with 
the overwrite paramater there to help. Also important to note that `setenv()` function is there to update or add
a variable in the environment of the calling process. The overwrite paramater take a zero or a non-zero variable. 
If the variable is a non-zero then it checks if the `name` is there in the environment, if it's not then it changes
the value of `name` to be the value of `value`. If the`overwrite` paramater is a zero then the value of `name` is
not changed. 

#####Return Value
The `setenv()` function returns zero on success, or -1 on error, with errno set to indicate the cause of the error.


#####Example
A char pointer variable pPath

``pPath = /class/classes/username/homefolder``

``"PWD" = /class/classes/username/homefolder/folder1``

Then the function is called as follows:

``setenv("PWD",pPath,1);``

Changes the value of `"PWD"` to be `/class/classes/username/homefolder`

``setenv("PWD",pPath,0);``

Does not change anything and leaves the value of `"PWD"` to be `/class/classes/username/homefolder`
