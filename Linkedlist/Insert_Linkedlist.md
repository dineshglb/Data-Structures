<p>
This code defines the three insertion functions and a main function to demonstrate the usage of these functions. 
It creates a linked list and performs insertions at the beginning, end, and after specific elements. The display function is used to print the linked list for verification.</p>

## Code

```c
#include <stdio.h>
#include <stdlib.h>

// Define the node structure
struct node {
    int data;
    struct node *next;
};

// Function to insert at the beginning of the linked list
struct node *insert_beg(struct node *head, int info) {
    struct node *new;
    new = (struct node *)malloc(sizeof(struct node));
    new->data = info;
    new->next = head;
    head = new;
    return head;
}

// Function to insert at the end of the linked list
struct node *insert_end(struct node *head, int info) {
    struct node *ptr, *new;
    new = (struct node *)malloc(sizeof(struct node));
    new->data = info;
    new->next = NULL;
    ptr = head;

    if (ptr != NULL) {
        while (ptr->next != NULL) {
            ptr = ptr->next;
        }
        ptr->next = new;
    } else {
        head = new;
    }

    return head;
}

// Function to insert after a specific element in the linked list
struct node *insert_after(struct node *head, int x, int info) {
    struct node *ptr, *new;
    new = (struct node *)malloc(sizeof(struct node));
    new->data = info;
    ptr = head;

    while (ptr != NULL && ptr->data != x) {
        ptr = ptr->next;
    }

    if (ptr != NULL) {
        new->next = ptr->next;
        ptr->next = new;
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

    return 0;
}
```
## Output

```c
Linked List after insert at the beginning:
30 -> 20 -> 10 -> NULL

Linked List after insert at the end:
30 -> 20 -> 10 -> 40 -> 50 -> NULL

Linked List after insert after a specific element:
30 -> 20 -> 25 -> 10 -> 40 -> 45 -> 50 -> NULL
```

