# Flattening a Nested List Using an Iterator
## DATE:
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

<img width="825" height="217" alt="image" src="https://github.com/user-attachments/assets/573787d5-b64f-4023-891a-349f8aef5fee" />



## Result:
The NestedIterator class successfully flattens a nested list of integers into a single list and provides sequential access using standard iterator methods.
