##setenv:

[man page](http://linux.die.net/man/3/setenv)

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

**Examples**

``char *ppath;`` is used as a variable in the following examples.

Example 1: This example shows what happens when the overwrite paramater is a non-zero and v_name has a value.

    ppath = getenv("PWD"); //gets the value of $PWD
    cout << "$PWD = " << ppath << endl;
    
    ppath = getenv("HOME"); //gets the value of the $HOME
    cout << "$HOME = " << ppath << endl;
    
    if(-1==setenv("PWD",ppath,1)) //since the overwrite paramater is non-zero it replaces value of
            cout << "error";                  //$PWD with the value of pPath which is defined as $HOME
    
    ppath = getenv("PWD");  //gets the value of $PWD
    cout << "$PWD = " << ppath << endl;     //the value should now be the same as the value of $HOME
  
Output 1:

    $PWD = /class/classes/dchou002/CS100
    $HOME = /class/classes/dchou002
    $PWD = /class/classes/dchou002

Example 2: This example shows what happens when the overwrite paramater is a non-zero and v_name does not have a value.

    if(-1==setenv("PWD","",1))      //makes the value of $PWD = ""
            cout << "error";
    
    ppath = getenv("PWD");          //puts the value of $PWD into pPath
    cout << "$PWD = " << ppath  << endl;
    
    ppath = getenv("HOME"); //gets the value of the $HOME
    cout << "$HOME = " << ppath << endl;
    
    if(-1==setenv("PWD",ppath,1)) //since the overwrite paramater is non-zero it replaces value of
            cout << "error";                  //$PWD with the value of pPath which is defined as $HOME
    
    ppath = getenv("PWD");  //gets the value of $PWD
    cout << "$PWD = " << ppath << endl;     //the value should now be the same as the value of $HOME

Output 2:

    $PWD =
    $HOME = /class/classes/dchou002
    $PWD = /class/classes/dchou002

Example 3: This example shows what happens when the overwrite paramater is a zero and v_name does have a value.

    ppath = getenv("PWD"); //gets the value of $PWD
    cout << "$PWD = " << ppath << endl;
    
    ppath = getenv("HOME"); //gets the value of the $HOME
    cout << "$HOME = " << ppath << endl;
    
    if(-1==setenv("PWD",ppath,0)) //since the overwrite paramater is non-zero it replaces value of
            cout << "error";                  //$PWD with the value of pPath which is defined as $HOME
    
    ppath = getenv("PWD");  //gets the value of $PWD
    cout << "$PWD = " << ppath << endl;     //the value should now be the same as the value of $HOME

Output 3:

    $PWD = /class/classes/dchou002/CS100
    $HOME = /class/classes/dchou002
    $PWD = /class/classes/dchou002/CS100

///////////////////////////////////////////

Example 4: This example shows what happens when the overwrite paramater is a zero and v_name is a paramater that is not defined in the environment.

    ppath = getenv("HOME"); //gets the value of the $HOME
    cout << "$HOME = " << ppath << endl;

    if(-1==setenv("random_name",ppath,0)) //since the overwrite paramater is non-zero it replaces value of
            cout << "error";                  //$PWD with the value of pPath which is defined as $HOME

    ppath = getenv("dom");  //gets the value of $PWD
    cout << "$random_name = " << ppath << endl;     //the value should now be the same as the value of $HOME

Output 4:

    $random_name = 
    $HOME = /class/classes/dchou002
    $random_name = /class/classes/dchou002
