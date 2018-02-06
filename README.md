# AOS_pj1
//char name[100]
/*
* Project 1.
* Create a struct named birthday with the following specifications
* a. Instead of using doulbe-linked lists, use a hash table with name as key.
* b. The table will use double-linked lists
* c. The buckets will use double-linked lists
* Due Feb 6 by 2PM.
*/

//my hash
/* This basic hash preforms a weighted calculation of the ASCII value of the
     character in the array, against an increasing weight based on the position
     the character has in the given string. */

#ifndef MYHASHATTEMPT_H
#define MYHASHATTEMPT_H

#ifdef __cplusplus
extern "C" {
#endif
#include <stdlib.h>



    int myHash(const char *a, int len){
    int temp;
    for(int i=0; i<len; i++)
    {
        temp+=a[i];
        temp*=(i+2);
    }
}



#ifdef __cplusplus
}
#endif

#endif /* MYHASHATTEMPT_H */
