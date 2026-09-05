# Ex8 Detection of Cycle and Finding the Starting Node in a Linked List
## DATE:
## AIM:
To write a program that detects a cycle in a linked list and returns the node where the cycle begins.
If there is no cycle, the program should return null without modifying the linked list.
## Algorithm
1. Initialize two pointers, slow and fast, at the head of the linked list.
2. Move the pointers through the list: advance slow by one node and fast by two nodes in each iteration.
3. Check for termination: if fast or fast.next becomes null, the list contains no cycle, so return null.
4. Detect the cycle: if slow and fast meet at the same node, a cycle exists in the linked list.
5. Find the start of the cycle: reset the slow pointer back to the head of the list, while keeping the fast pointer at the meeting node.
6. Advance both pointers one node at a time simultaneously until they meet again.
7. Return the meeting node, which is the exact starting node of the cycle.


## Program:
```
/*
program that detects a cycle in a linked list and returns the node where the cycle begins.
If there is no cycle, the program should return null without modifying the linked list.
Developed by: MUHAMMAD ASJAD E
RegisterNumber:  212225240091
*/
```

```
import java.util.Scanner;
import java.util.HashMap;

class ListNode {
    int val;
    ListNode next;
    ListNode(int x) {
        val = x;
        next = null;
    }
}

public class Main {
    // Method to detect cycle and return the starting node
    public static ListNode detectCycle(ListNode head) {
        if (head == null || head.next == null) {
            return null;
        }

        ListNode slow = head;
        ListNode fast = head;

        // Step 1: Detect if a cycle exists
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;

            if (slow == fast) {
                // Step 2: Find the starting node of the cycle
                slow = head;
                while (slow != fast) {
                    slow = slow.next;
                    fast = fast.next;
                }
                return slow; // Starting node of the cycle
            }
        }

        return null; // No cycle found
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter the number of nodes: ");
        int n = scanner.nextInt();

        if (n <= 0) {
            System.out.println("The list is empty. No cycle possible.");
            scanner.close();
            return;
        }

        System.out.println("Enter the values of the nodes separated by spaces: ");
        ListNode head = null;
        ListNode tail = null;
        
        // Map to keep track of nodes by their 0-indexed position to create a cycle easily
        HashMap<Integer, ListNode> nodeMap = new HashMap<>();

        for (int i = 0; i < n; i++) {
            int value = scanner.nextInt();
            ListNode newNode = new ListNode(value);
            nodeMap.put(i, newNode);

            if (head == null) {
                head = newNode;
                tail = newNode;
            } else {
                tail.next = newNode;
                tail = newNode;
            }
        }

        System.out.print("Enter the 0-indexed position to connect the tail to (enter -1 for no cycle): ");
        int cyclePos = scanner.nextInt();

        // If cyclePos is valid, connect the tail node to that specific node
        if (cyclePos >= 0 && cyclePos < n) {
            tail.next = nodeMap.get(cyclePos);
            System.out.println("Cycle successfully created linking tail back to node at index " + cyclePos);
        } else {
            System.out.println("No cycle created. The linked list is linear.");
        }

        // Run the algorithm
        ListNode startNode = detectCycle(head);

        // Output results
        if (startNode != null) {
            System.out.println("Cycle detected! The starting node of the cycle has a value of: " + startNode.val);
        } else {
            System.out.println("No cycle detected in the linked list.");
        }

        scanner.close();
    }
}

```
## Output:

<img width="852" height="312" alt="image" src="https://github.com/user-attachments/assets/07f9f098-3fd3-4d6c-8e2d-5ad311c2a474" />


## Result:
The program successfully detects whether a cycle exists in the linked list.
If a cycle is present, it correctly identifies and returns the node where the cycle begins.
