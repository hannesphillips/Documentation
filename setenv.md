##setenv:

[man page - setenv](http://linux.die.net/man/3/setenv)

**includes:** `#include <stdlib.h>`

**declaraton:** `int setenv(const char *v_name, const char *v_value, int overwrite);`

**returns:** If successful returns zero, otherwise returns -1, with errno set to indicate the cause of the error.

**overwrite paramater:**

######Nonzero

- Change the existing entry of v_name.
- If v_name is defined and exists, the value of v_name is changed to the v_value. 
- If v_name was previously undefined, it is given the value of v_value. 

######Zero
  
- Do not change the existing entry of v_name.
- If v_name is defined and exists, the value of v_name is *not* changed to the v_value. 
- If v_name was previously undefined, it is given the value of v_value. 

##getenv:

[man page - getenv](http://linux.die.net/man/3/getenv)

**includes:** `#include <stdlib.h>`

**declaraton:** `char *getenv(const char *name)`

**returns:**  If successful returns a pointer to the value in the environment, or NULL if there is no match.

##Examples

``char *ppath`` is used as a variable in the following examples.

Example 1: This example shows what happens when the overwrite paramater is a non-zero and v_name has a value.

    ppath = getenv("PWD");                  //puts the environment of $PWD into ppath
    if(ppath == NULL)                       //error checking
      perror("getenv");   
    cout << "$PWD = " << ppath << endl;     //prints the environment of $PWD 
    
    ppath = getenv("HOME");                 //gets the environment of the $HOME
    if(ppath == NULL)                       //error checking
      perror("getenv");
    cout << "$HOME = " << ppath << endl;    //prints the environment of $PWD
    
    if(-1==setenv("PWD",ppath,1))           //since the overwrite paramater is non-zero it replaces environment 
      perror("setenv");                     //of $PWD with the value of ppath which is defined by the environment 
                                            //of $HOME
    
    ppath = getenv("PWD");                  //gets the environment of $PWD
    if(ppath == NULL)                       //error checking
      perror("getenv");
    cout << "$PWD = " << ppath << endl;     //the value should now be the same as the value of $HOME
  
Output 1:

    $PWD = /class/classes/dchou002/CS100
    $HOME = /class/classes/dchou002
    $PWD = /class/classes/dchou002

Example 2: This example shows what happens when the overwrite paramater is a non-zero and v_name does not have a value.

    ppath = getenv("PWD");                  
    if(ppath == NULL)
      perror("getenv");
    cout << "$PWD = " << ppath  << endl;    //in this case ppath ="" because the environment of $PWD is not set
    
    ppath = getenv("HOME"); 
    if(ppath == NULL)
      perror("getenv");
    cout << "$HOME = " << ppath << endl;
    
    if(-1==setenv("PWD",ppath,1))           //since the overwrite paramater is non-zero it replaces environment 
      perror("setenv");                     //of $PWD with the value of ppath which is defined by the environment 
                                            //of $HOME 
    
    ppath = getenv("PWD");                  
    if(ppath == NULL)
      perror("getenv");  
    cout << "$PWD = " << ppath << endl;     //the value should now be the same as the value of $HOME

Output 2:

    $PWD =
    $HOME = /class/classes/dchou002
    $PWD = /class/classes/dchou002

Example 3: This example shows what happens when the overwrite paramater is a zero and v_name does have a value.

    ppath = getenv("PWD"); 
    if(ppath == NULL)
      perror("getenv");
    cout << "$PWD = " << ppath << endl;
    
    ppath = getenv("HOME"); 
    if(ppath == NULL)
      perror("getenv");
    cout << "$HOME = " << ppath << endl;
    
    if(-1==setenv("PWD",ppath,0))           //since the overwrite paramater is zero it does not replaces  
      perror("setenv");                     //environment of $PWD with ppath.
    
    ppath = getenv("PWD");                
    if(ppath == NULL)
      perror("getenv");
    cout << "$PWD = " << ppath << endl;     //the value should not be changed.

Output 3:

    $PWD = /class/classes/dchou002/CS100
    $HOME = /class/classes/dchou002
    $PWD = /class/classes/dchou002/CS100

///////////////////////////////////////////

Example 4: This example shows what happens when the overwrite paramater is a zero *or* a non-zero and v_name is a paramater that is not defined in the environment.

    ppath = getenv("HOME"); 
    if(ppath == NULL)
      perror("getenv");
    cout << "$HOME = " << ppath << endl;

    if(-1==setenv("random_name",ppath,0))   //since the overwrite paramater is zero and the the variable     
    perror("setenv");                       //$random_name is undefined, setenv makes the environment of 
                                            //$random_variable be the value of ppath. If the case where
                                            //there is a undefined variable the setenv behavous the
                                            //same way regardless of a non-zero or zero overwrite paramater. 
                                            
    ppath = getenv("random_name");  //gets the value of $PWD
    if(ppath == NULL)
      perror("getenv");
    cout << "$random_name = " << ppath << endl;     //the value should now be the same as the value of $HOME

Output 4:

    $HOME = /class/classes/dchou002
    $random_name = /class/classes/dchou002
