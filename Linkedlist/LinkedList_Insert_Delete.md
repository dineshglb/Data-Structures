
```c
#include <stdio.h>
#include <stdlib.h>

// Define the node structure
struct node {
    int data;
    struct node *next;
};

// Function to insert at the beginning of the linked list
struct node* insert_beg(struct node *head, int info) {
    struct node *newNode;
    newNode = (struct node *)malloc(sizeof(struct node));
    newNode->data = info;
    newNode->next = head;
    head = newNode;
    return head;
}

// Function to insert at the end of the linked list
struct node* insert_end(struct node *head, int info) {
    struct node *ptr, *newNode;
    newNode = (struct node *)malloc(sizeof(struct node));
    newNode->data = info;
    newNode->next = NULL;
    ptr = head;

    if (ptr != NULL) {
        while (ptr->next != NULL) {
            ptr = ptr->next;
        }
        ptr->next = newNode;
    } else {
        head = newNode;
    }

    return head;
}

// Function to insert after a specific element in the linked list
struct node* insert_after(struct node *head, int x, int info) {
    struct node *ptr, *newNode;
    newNode = (struct node *)malloc(sizeof(struct node));
    newNode->data = info;
    ptr = head;

    while (ptr != NULL && ptr->data != x) {
        ptr = ptr->next;
    }

    if (ptr != NULL) {
        newNode->next = ptr->next;
        ptr->next = newNode;
    }

    return head;
}

// Function to delete a node after a specific element
struct node* del_after(struct node *head, int del) {
    struct node *ptr1, *ptr2;
    ptr1 = head;

    while (ptr1->next != NULL) {
        if (ptr1->data == del) {
            ptr2 = ptr1->next;
            ptr1->next = ptr2->next;
            free(ptr2);
            break; // Assuming you want to delete only the first occurrence
        }
        ptr1 = ptr1->next;
    }

    return head;
}

// Function to delete the last node
struct node* del_end(struct node *head) {
    struct node *ptr, *prevp;

    if (head == NULL) {
        printf("List is Empty");
    } else if (head->next == NULL) {
        free(head);
        head = NULL;
    } else {
        ptr = head;
        while (ptr->next != NULL) {
            prevp = ptr;
            ptr = ptr->next;
        }
        prevp->next = NULL;
        free(ptr);
    }

    return head;
}

// Function to display the linked list
void display(struct node *head) {
    struct node *ptr = head;
    while (ptr != NULL) {
        printf("%d -> ", ptr->data);
        ptr = ptr->next;
    }
    printf("NULL\n");
}

int main() {
    struct node *head = NULL;

    // Insert at the beginning
    head = insert_beg(head, 10);
    head = insert_beg(head, 20);
    head = insert_beg(head, 30);

    printf("Linked List after insert at the beginning:\n");
    display(head);

    // Insert at the end
    head = insert_end(head, 40);
    head = insert_end(head, 50);

    printf("Linked List after insert at the end:\n");
    display(head);

    // Insert after a specific element
    head = insert_after(head, 20, 25);
    head = insert_after(head, 40, 45);

    printf("Linked List after insert after a specific element:\n");
    display(head);

    // Delete after a specific element
    head = del_after(head, 20);
    printf("Linked List after deleting after a specific element:\n");
    display(head);

    // Delete the last node
    head = del_end(head);
    printf("Linked List after deleting the last node:\n");
    display(head);

    return 0;
}
```
