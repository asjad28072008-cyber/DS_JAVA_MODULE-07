# Ex7 Removal of Nodes with a Specific Value from a Linked List
## DATE:
## AIM:
To write a java  program that removes all nodes from a linked list whose value matches a given integer (val) and returns the new head of the modified linked list.

## Algorithm
1. Create a dummy node that points to the head of the linked list to easily handle edge cases where the head node itself needs to be removed.
2. Initialize a current pointer to point to the dummy node.
3. Traverse the linked list using a loop that continues as long as current.next is not null.
4. Check the next node's value: If current.next.val equals the given integer val, skip the node by setting current.next = current.next.next. Otherwise, advance the current pointer to current.next.
5. Return the new head of the modified linked list, which is located at dummy.next.


## Program:
```
/*
program that removes all nodes from a linked list whose value matches a given integer (val) and returns the new head of the modified linked list.
Developed by: MUHAMMAD ASJAD E
RegisterNumber:  212225240091
*/
```


```

import java.util.Scanner;

public class RemoveLinkedListElements {
    
    // Nested static class so it belongs to RemoveLinkedListElements
    static class ListNode {
        int val;
        ListNode next;
        
        ListNode(int val) {
            this.val = val;
            this.next = null;
        }
    }
    
    // Method to remove all elements matching the target value
    public static ListNode removeElements(ListNode head, int val) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode current = dummy;
        
        while (current.next != null) {
            if (current.next.val == val) {
                current.next = current.next.next;
            } else {
                current = current.next;
            }
        }
        return dummy.next;
    }

    // Helper method to print the linked list
    public static void printList(ListNode head) {
        if (head == null) {
            System.out.println("Empty List (null)");
            return;
        }
        ListNode current = head;
        while (current != null) {
            System.out.print(current.val + " -> ");
            current = current.next;
        }
        System.out.println("null");
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Enter the number of nodes: ");
        int n = scanner.nextInt();
        
        ListNode head = null;
        ListNode tail = null;
        
        if (n > 0) {
            System.out.println("Enter the values for the nodes:");
            for (int i = 0; i < n; i++) {
                int value = scanner.nextInt();
                ListNode newNode = new ListNode(value);
                
                if (head == null) {
                    head = newNode;
                    tail = newNode;
                } else {
                    tail.next = newNode;
                    tail = newNode;
                }
            }
        }
        
        System.out.print("Enter the value to remove: ");
        int targetValue = scanner.nextInt();
        
        System.out.print("\nOriginal List: ");
        printList(head);
        
        head = removeElements(head, targetValue);
        
        System.out.print("Modified List: ");
        printList(head);
        
        scanner.close();
    }
}

```
## Output:

<img width="640" height="492" alt="image" src="https://github.com/user-attachments/assets/95dc702e-4a8c-4f6d-849d-08ffd2d59f26" />


## Result:
The java program successfully removes all nodes with the specified value (val) from the linked list and returns the new head.
