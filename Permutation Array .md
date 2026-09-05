# Ex9 Finding the Longest Length of Nested Set in a Permutation Array
## DATE:
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

<img width="807" height="435" alt="image" src="https://github.com/user-attachments/assets/b2dc953c-2f1b-4d39-9fb8-e245514548e6" />


## Result:
The program successfully computes the longest length of the nested set s[k] for the given permutation array.
