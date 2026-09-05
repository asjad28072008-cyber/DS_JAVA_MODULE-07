# Ex6 Right Rotation LinkedList
## DATE:
## AIM:
To write a Java  program to:
Create a singly linked list.
Rotate the linked list to the right by k positions.
Display the rotated linked list.
## Algorithm
1. 
2. 
3. 
4.  
5.   

## Program:
```
/*
Program to  Right Rotation LinkedList
Developed by: MUHAMMAD ASJAD E
RegisterNumber:  212225240091
*/
```

```

import java.util.Scanner;

public class Node {
    int data;
    Node next;

    // Constructor for individual nodes
    Node(int data) {
        this.data = data;
        this.next = null;
    }

    private static Node head = null;
    private static Node tail = null;

    // Method to add a new node to the linked list
    public static void insert(int data) {
        Node newNode = new Node(data);
        if (head == null) {
            head = newNode;
            tail = newNode;
        } else {
            tail.next = newNode;
            tail = newNode;
        }
    }

    // Method to rotate the linked list to the right by k positions
    public static void rotateRight(int k) {
        if (head == null || head.next == null || k == 0) {
            return;
        }

        // 1. Calculate length and find the tail node
        Node current = head;
        int length = 1;
        while (current.next != null) {
            current = current.next;
            length++;
        }

        // 2. Adjust k if it exceeds the length
        k = k % length;
        if (k == 0) {
            return;
        }

        // 3. Connect tail to head to form a loop
        current.next = head;

        // 4. Find the new tail node at position (length - k)
        int stepsToNewTail = length - k;
        Node newTail = head;
        for (int i = 1; i < stepsToNewTail; i++) {
            newTail = newTail.next;
        }

        // 5. Update head and break the circular connection
        head = newTail.next;
        newTail.next = null;
    }

    // Method to display the linked list
    public static void display() {
        if (head == null) {
            System.out.println("List is empty.");
            return;
        }
        Node current = head;
        while (current != null) {
            System.out.print(current.data + " -> ");
            current = current.next;
        }
        System.out.println("null");
    }

    // Main method is now inside the Node class to fix your error
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter the number of elements in the linked list: ");
        int n = scanner.nextInt();

        System.out.println("Enter the elements:");
        for (int i = 0; i < n; i++) {
            insert(scanner.nextInt());
        }

        System.out.print("Enter the number of positions to rotate (k): ");
        int k = scanner.nextInt();

        System.out.println("\nOriginal Linked List:");
        display();

        rotateRight(k);

        System.out.println("\nRotated Linked List:");
        display();

        scanner.close();
    }
}

```

## Output:

<img width="671" height="630" alt="image" src="https://github.com/user-attachments/assets/e1886a6f-13fd-4538-b811-0d98ebca3786" />



## Result:
Thus, the C program to perfom right rotation on linked list is implemented successfully.
