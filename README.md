# Ex6 Right Rotation LinkedList
## DATE: 25.08.2026
## AIM:
To write a Java  program to:
Create a singly linked list.
Rotate the linked list to the right by k positions.
Display the rotated linked list.
## Algorithm
1. Calculate the length (\(n\)) of the linked list by traversing it while keeping track of the tail node.
2. Handle base cases: If the list is empty (head == null), contains only one node (head.next == null), or \(k = 0\), return the head immediately.
3. Optimize \(k\): Update \(k = k \pmod n\). If \(k = 0\) after this operation, no rotation is needed; return the original head.
4. Form a loop: Connect the tail node's next pointer to the original head node, making the list circular.
5. Locate the new split point: Traverse \(n - k\) steps from the original head to find the new tail node of the rotated list.
6. Break the loop: Set the head to newTail.next, and then set newTail.next = null to terminate the circular connection.

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


<img width="950" height="233" alt="image" src="https://github.com/user-attachments/assets/91d278b1-9c56-4522-8758-c25b5a21a831" />



## Result:
Thus, the C program to perfom right rotation on linked list is implemented successfully.



























# Ex7 Removal of Nodes with a Specific Value from a Linked List
## DATE: 25.08.2026
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

<img width="632" height="187" alt="image" src="https://github.com/user-attachments/assets/aa8cc46b-3a12-4d21-aa6e-9e209f0b4e09" />



## Result:
The java program successfully removes all nodes with the specified value (val) from the linked list and returns the new head.




















# Ex8 Detection of Cycle and Finding the Starting Node in a Linked List
## DATE: 25.08.2026
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

<img width="882" height="181" alt="image" src="https://github.com/user-attachments/assets/1ab469db-fdac-473f-b6d7-ecd6a97668fe" />



## Result:
The program successfully detects whether a cycle exists in the linked list.
If a cycle is present, it correctly identifies and returns the node where the cycle begins.

























# Ex9 Finding the Longest Length of Nested Set in a Permutation Array
## DATE: 25.08.2026
## AIM:
To write a program that finds the length of the longest set s[k] defined as s[k] = { nums[k], nums[nums[k]], nums[nums[nums[k]]], … },where the iteration stops before a duplicate element occurs.

The task is to return the maximum size among all such sets.
## Algorithm
1. Initialize a variable max_length = 0 to store the maximum size of any nested set found.
2. Iterate through each index i of the array from 0 to n - 1.
3. Check if the current element at index i has been visited. If nums[i] is already marked (e.g., set to -1), skip it to avoid re-processing the same cycle.
4. Traverse the cycle starting from index i. Keep track of the current cycle's length, and mark each visited element by changing its value to -1 until a previously visited element or a duplicate is encountered.
5. Update max_length with the maximum of its current value and the length of the found cycle, then return max_length once all elements are checked.


## Program:
```
/*
Program to find the Longest Length of Nested Set in a Permutation Array
Developed by: MUHAMMAD ASJAD E
RegisterNumber:  212225240091
*/
```

```

import java.util.Scanner;

public class ArrayNesting {

    public static int arrayNesting(int[] nums) {
        int maxLength = 0;

        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != -1) {
                int start = nums[i];
                int count = 0;

                while (nums[start] != -1) {
                    int temp = start;
                    start = nums[start]; 
                    nums[temp] = -1;     
                    count++;             
                }
                maxLength = Math.max(maxLength, count);
            }
        }
        return maxLength;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter the number of elements in the permutation array: ");
        int n = scanner.nextInt();

        int[] nums = new int[n];
        System.out.println("Enter the elements (numbers must strictly be between 0 and " + (n - 1) + "):");
        
        for (int i = 0; i < n; i++) {
            int input = scanner.nextInt();
            
            // Validation check to prevent the ArrayIndexOutOfBoundsException
            if (input < 0 || input >= n) {
                System.out.println("\nERROR: Value " + input + " is out of bounds! " +
                                   "Elements must be between 0 and " + (n - 1) + ".");
                System.exit(0); // Safely stop the program
            }
            
            nums[i] = input;
        }

        int result = arrayNesting(nums);
        System.out.println("\nThe maximum size among all nested sets is: " + result);

        scanner.close();
    }
}

```
## Output:

<img width="480" height="85" alt="image" src="https://github.com/user-attachments/assets/70c47a06-4abd-4da6-bb56-2bd07025d546" />



## Result:
The program successfully computes the longest length of the nested set s[k] for the given permutation array.
























# Flattening a Nested List Using an Iterator
## DATE: 25.08.2026
## AIM:
To design and implement a class NestedIterator that flattens a nested list of integers such that all integers can be accessed sequentially using an iterator interface (next() and hasNext()).
## Algorithm
1. Initialization: In the constructor, initialize a stack data structure and push all elements of the input nested list onto it from right to left (reverse order) so that the first element of the list sits at the top of the stack.
2. Implement hasNext() Check: When hasNext() is called, enter a loop that runs as long as the stack is not empty to inspect the top element.
3. Handle Lists in hasNext(): If the top element of the stack is a nested list, pop it from the stack and push all of its inner elements onto the stack in reverse order, then continue the loop.
4. Confirm Integer Presence: If the top element is an integer, immediately break the loop and return true. If the stack becomes empty after processing all elements, return false.
5. Implement next() Retrieval: In the next() method, call hasNext() to ensure the top element is a flattened integer, then pop and return that integer from the top of the stack.


## Program:
```
/*
Program to find Flattening a Nested List Using an Iterator
Developed by: MUHAMMAD ASJAD E
RegisterNumber:  212225240091
*/
```

```
import java.util.*;

// Interface representing either a single integer or a nested list
interface NestedInteger {
    boolean isInteger();
    Integer getInteger();
    List<NestedInteger> getList();
}

// Concrete implementation of NestedInteger for the program
class NestedIntegerImpl implements NestedInteger {
    private Integer integerValue;
    private List<NestedInteger> listValue;

    public NestedIntegerImpl(int value) {
        this.integerValue = value;
        this.listValue = null;
    }

    public NestedIntegerImpl(List<NestedInteger> list) {
        this.integerValue = null;
        this.listValue = list;
    }

    @Override
    public boolean isInteger() {
        return integerValue != null;
    }

    @Override
    public Integer getInteger() {
        return integerValue;
    }

    @Override
    public List<NestedInteger> getList() {
        return listValue;
    }
}

// The Iterator Implementation
class NestedIterator implements Iterator<Integer> {
    private Deque<NestedInteger> stack;

    public NestedIterator(List<NestedInteger> nestedList) {
        stack = new ArrayDeque<>();
        // Push elements from right to left so the first element is at the top
        for (int i = nestedList.size() - 1; i >= 0; i--) {
            stack.push(nestedList.get(i));
        }
    }

    @Override
    public Integer next() {
        // hasNext() guarantees the top element is a single integer
        if (!hasNext()) {
            throw new NoSuchElementException();
        }
        return stack.pop().getInteger();
    }

    @Override
    public boolean hasNext() {
        // Flatten the top of the stack until an integer is reached or stack is empty
        while (!stack.isEmpty()) {
            NestedInteger curr = stack.peek();
            if (curr.isInteger()) {
                return true;
            }
            // If it's a list, pop it and push its contents in reverse order
            stack.pop();
            List<NestedInteger> list = curr.getList();
            for (int i = list.size() - 1; i >= 0; i--) {
                stack.push(list.get(i));
            }
        }
        return false;
    }
}

// Main class to handle user input and run the iterator
public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.println("Enter a nested list string (e.g., [[1,1],2,[1,1]] or [1,[4,[6]]]):");
        String input = scanner.nextLine().trim();
        
        try {
            List<NestedInteger> nestedList = parseInput(input);
            NestedIterator iterator = new NestedIterator(nestedList);
            
            System.out.print("Flattened list output: ");
            List<Integer> result = new ArrayList<>();
            while (iterator.hasNext()) {
                result.add(iterator.next());
            }
            System.out.println(result);
            
        } catch (Exception e) {
            System.out.println("Error parsing input. Please make sure the brackets and commas match standard format.");
        } finally {
            scanner.close();
        }
    }

    // Helper method to parse a string into a List of NestedInteger
    private static List<NestedInteger> parseInput(String s) {
        if (s == null || s.isEmpty()) return new ArrayList<>();
        
        Deque<List<NestedInteger>> stack = new ArrayDeque<>();
        List<NestedInteger> currentList = new ArrayList<>();
        StringBuilder numberBuffer = new StringBuilder();

        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);

            if (c == '[') {
                if (i > 0) {
                    stack.push(currentList);
                    currentList = new ArrayList<>();
                }
            } else if (c == ']' || c == ',') {
                if (numberBuffer.length() > 0) {
                    currentList.add(new NestedIntegerImpl(Integer.parseInt(numberBuffer.toString())));
                    numberBuffer.setLength(0);
                }
                if (c == ']' && !stack.isEmpty()) {
                    List<NestedInteger> parentList = stack.pop();
                    parentList.add(new NestedIntegerImpl(currentList));
                    currentList = parentList;
                }
            } else if (Character.isDigit(c) || c == '-') {
                numberBuffer.append(c);
            }
        }
        return currentList;
    }
}

```

## Output:

<img width="652" height="81" alt="image" src="https://github.com/user-attachments/assets/d753cd42-fa51-43ef-a07d-745eadb549bf" />




## Result:
The NestedIterator class successfully flattens a nested list of integers into a single list and provides sequential access using standard iterator methods.
