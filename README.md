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

#include <stdio>
#include <stdlib>
#include "list.h"

struct birthday {
  char name[100];
  int day;
  int month;
  int year;
  /*
  * (kernel lisked list format)
  * list.h will connect this statement and will provide the doubly linked lists
  * capability
  */
  struct list_head list;
}
