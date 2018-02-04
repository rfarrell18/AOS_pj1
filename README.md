# AOS_pj1
//char name[100]
/*
* Project 1.
* Create a struct named birthday with the following specifications
* a. Instead of using doubly-linked lists, use a hash table with name as key.
* b. The table will use double-linked lists
* c. The buckets will use double-linked lists
* Due Feb 6 by 2PM.

/*
 * This program is part of an ongoing build for AOS. In this version the nodes
 * of the given struct are able to print after being populated. This "section"
 * of the program will eventually represent the third part of a hash table,
 * loosely speaking.
 */

/*
 * Test File:   main.cpp
 * Author: Rich
 * For AOS
 * Latest Build Created on Saturday February 3, 2018, 7:57 PM - 3AM
 */

#include <stdlib.h>
#include <stdio.h>



    struct birthday
    {
        struct birthday *next; //used to move around DLL
        struct birthday *prev;
        //each copy of struct or node will can have a name up to 100 characters in length
        char name[100];
        int day;
        int month;
        int year;

        /* still working on this...I am able to link it from the test file
         * list.h but still trying to link all the functions that need to be
         * called to push the DLL capability to a header file */
        //struct list_head list;
    };

    //print the contents of the DLL list starting from given node
    void printList(struct birthday *node)
    {
        struct birthday *last;
        printf("\nPrint forward direction \n");
        while (node != NULL)
        {
            printf("%s ", node->name);
            printf(" %d ", node->day);
            printf(" %d ", node->month);
            printf(" %d ", node->year);

            last = node;
            node = node->next;
        }
    }

    void bdayAppend(struct birthday** head_ref, char nme[], int dy, int mnth, int yr)
    {
        //make new node by allocating enough memory that is as big as the struct
         struct birthday* new_node = (struct birthday*) malloc(sizeof(struct birthday));
         struct birthday *last = *head_ref;

         //load struct elements passed by function to newly created node
         for(int i=0; i<100; i++){
         new_node->name[i] = nme[i];}
         new_node->day = dy;
         new_node->month = mnth;
         new_node->year = yr;
         new_node->next = NULL;
        if(*head_ref == NULL)
        {
             new_node->prev = NULL;
            *head_ref = new_node;
            return;
        }

        // Else traverse till the last node
         while(last->next != NULL)
        {
             last = last->next;
        }

        //change the next of last node
         last->next = new_node;
         new_node->prev = last;
        return;
    }

    //Delete a node after given day of birth, will expand to names as well
    //less likely that two people with the same name will have the same birthday
    void deleteNode(struct birthday **head_ref, int key)
    {
        //store head node
        struct birthday* temp = *head_ref, *prev;

        //if head node holds the key to be deleted
        if (temp!=NULL && temp->day == key)
        {
            *head_ref = temp->next; //changed head
            free(temp); //free memory allocated to old head
            return;
        }
        //search for key to be deleted, keep track of the previous node
        //need to change pre_next
        //expand for more than one struct member***
        while(temp!= NULL && temp->day!=key)
        {
            prev = temp;
            temp = temp->next;
        }
        //if key was not present in linked list
        if(temp==NULL) return;

        //unlink the node from linked list
        prev->next = temp->next;
        free(temp); //free memory
    }


int main(int argc, char** argv) {

    //DLL working
    char e[]="Tairiq Jones"; //test array
    char f[]="Daryl Michealson";//test array
    //initialize head to point to nothing - empty list
    struct birthday* head = NULL;
    bdayAppend(&head, f, 4, 12, 18);
    bdayAppend(&head, e, 3, 9, 2018);
    printf("Created DLL is: ");
    printList(head);
    deleteNode(&head, 4);
    printf("Adjusted DLL after deleting first node: ");
    printList(head);
    //getchar(); //..will use for later testing
    return 0;
}
