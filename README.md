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
 * Phase 1.0 - HashTable - Buckets
 * Created on February 6, 2018, 12:37 AM
 */

#include <stdio.h>
#include <stdlib.h>
#include "list.h"

struct birthday {
    char name[100]; //key
    int day;
    int month;
    int year;
    struct list_head list;
};
/*
 *
 */
int main(int argc, char** argv) {
    struct birthday *tmp; //holds the address of a newly created node
    struct list_head *pos; //position / for loop control number
    struct list_head *q;
    unsigned int i;
    struct birthday myList; //

    INIT_LIST_HEAD(&myList.list);//declares and initializes the list
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
    }
    printf("\n");

    list_for_each(pos, &myList.list){
        tmp = list_entry(pos, struct birthday, list);
        printf("Name: %s  Day: %d  Month: %d  Year: %d", tmp->name, tmp->day, tmp->month, tmp->year);
        printf("\n");
    }
    printf("\n");

        printf("Deleting the list using list_for_each_safe()\n");
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
