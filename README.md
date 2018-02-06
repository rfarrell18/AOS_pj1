/*
 * This file in its current state uses the given structure to create a
 * Linux kernel DDL (circular list). It accepts 3 First names, day, month year
 * with one space in between. It prints the list, then deletes the list by
 * freeing the memory that it dynamically allocated to each list item. 6:32AM
 *
 * Next phase is to connect this with the HashTable & HashFunction
 */

/*
 * File:   main.c
 * Author: RFarrell
 * Project: Kenel Programming 1
 * Phase 1.1 - Hash - Buckets
 * Created on February 6, 2018, 12:37 AM
 */
 /*
  * This file in its current state uses the given structure to create a
  * Linux kernel DDL (circular list). It accepts 3 First names, day, month year
  * with one space in between. It prints the list, then deletes the list by
  * freeing the memory that it dynamically allocated to each list item. 6:32AM
  *
  * Next phase is to connect this with the HashTable & HashFunction
  */

 /*
  * File:   main.c
  * Author: RFarrell
  * Project: Kenel Programming 1
  * Created on February 6, 2018, 12:37 AM
  */

 #include <stdio.h>
 #include <stdlib.h>
 #include <string.h>
 #include "list.h"

 struct birthday {
     char name[100]; //key
     int day;
     int month;
     int year;
     struct list_head list;
 };

 struct hashEntry {
     int NameHashKey[100];

     struct list_head list;
 };





 /*
  *
  */
 int main(int argc, char** argv) {
     struct birthday *tmp; //holds the address of a newly created node
     struct list_head *pos; //position / for loop control number
     struct list_head *q;
     int NumOfBuckets = 30;
     unsigned int i;
     unsigned int j; //list count
     int k, POSID;
     struct birthday myList;
     struct hashEntry myHashList;//
     char searchFor[100];
     int hash;


    //int myHash(const char *a, int len);
     /* This basic hash preforms a weighted calculation of the ASCII value of the
      * character in the array, against an increasing weight based on the position
      * the character has in the given string
      * Created on February 4, 2018, 10:13 PM */
   /*
     int myHash(const char &a, int len){
     int hash;
     for(int i=0; i<len; i++)
     {
         hash+=a[i];
         hash*=(i+2);
     }
     return hash;
 }
 */

     INIT_LIST_HEAD(&myList.list);//declares and initializes the list
     INIT_LIST_HEAD(&myHashList.list);
     //LIST_HEAD(myList);
     //Adding elements to the list

     //dynamically allocate memory in the size of the struct birthday
     //return the pointer to this new struct memory area to the pointer tmp
     for(i=3; i!=0; --i){
     tmp = (struct birthday *)malloc(sizeof(struct birthday));
     INIT_LIST_HEAD(&tmp->list); //initialize the dynamically allocated list head
     printf("Enter the Name, Day, Month, and Year: ");
     scanf("%s %d %d %d", &tmp->name, &tmp->day, &tmp->month, &tmp->year);


     /* Add the new item pointed to by the pointer tmp to the list of items
      in mylist */
     list_add(&(tmp->list), &(myList.list));
     j++;
     }
     printf("\n");

     //returns a pointer to a particular list item and places it in tmp
     /*for search, use this same functions and alter it to use tmp->name
      as an input to hash*/
     list_for_each(pos, &myList.list){
         tmp = list_entry(pos, struct birthday, list);
         printf("Name: %s  Day: %d  Month: %d  Year: %d", tmp->name, tmp->day, tmp->month, tmp->year);
         printf("\n");
         printf("tmp pointer: %d\n", tmp);

     }
     printf("\n");
     //printf("%s", searchFor);

     printf("Enter the Name to search for: ");
     scanf("%s", searchFor);

     //switch statement
     switch (1){
         case 1:

             for(int i=0; i<strlen(searchFor); i++)
                 {
                     hash+=searchFor[i];
                     hash*=(i+2);
                 }
             POSID = hash%NumOfBuckets;
             printf("Hash= %d\nRecord in Bucket=%d\n ", hash,POSID);
             break;
         default:
             printf("The entered name is not associated with this list");
     }
     /******for search, use this same functions and alter it to use tmp->name
      as an input to hash*/
     /*
     list_for_each(pos, &myHashList.list){
         tmp = list_entry(pos, struct hashEntry, list);
         //REMEMBER THE RESULT OF THE HASH MUST BE ASSOCIATED WITH A NUMBER
         //THAT NUMBER REPRESENTS THE POSITION OF THE DATA BEING LOOKED FOR
         //THAT IS WHY YOU HAVE TO MOD
         //keep count of how many entries, that is your mod*
      if((searchFor == tmp->name)&&(hashresult%numberOfItems)){
         printf("Name: %s  Day: %d  Month: %d  Year: %d", tmp->name, tmp->day, tmp->month, tmp->year);
         printf("\n");
         }
      }
     */
     printf("\n");

         printf("\nDeleting the list using list_for_each_safe()\n");
         list_for_each_safe(pos, q, &myList.list){
             tmp=list_entry(pos, struct birthday, list);
             printf("Freeing item Name: %s  Day: %d  Month: %d  Year: %d", tmp->name, tmp->day, tmp->month, tmp->year);
             printf("\n");
             list_del(pos);
             free(tmp);
         }






     //EXIT_SUCCESS
     return (0);
 }
