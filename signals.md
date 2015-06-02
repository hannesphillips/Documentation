#Sigaction System Call


This file will include information pertaining to 'sigaction'. 


##sigaction:

**includes: ** '#include <signal.h>'

**declaration: ** 'int sigaction(int signum, const struct sigaction *act, struct sigaction *oldact);'

**returns: ** will return 0 on success if the signal action has been changed. -1 is returned if an error has occured. 

[man page](http://man7.org/linux/man-pages/man2/sigaction.2.html)

The sigaction system call is very important to understand to properly modify signals. 

'sigaction' is used to change the action taken by a process on receipt of a specfic signal. This is a lot more comprehensive way to control signals; a lot of new actions should use 'sigaction()' rather than 'signal()'. 


Some good example code can be shown below.


