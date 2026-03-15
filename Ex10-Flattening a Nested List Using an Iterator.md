# Flattening a Nested List Using an Iterator
## DATE: 28.1.26
## AIM:
To design and implement a class NestedIterator that flattens a nested list of integers such that all integers can be accessed sequentially using an iterator interface (next() and hasNext()).
## Algorithm
1. Start the program.  
2. Define an interface-like class `NestedInteger` that can represent either a single integer or a nested list.  
3. Use a stack or recursion to flatten all integers from the nested list into a single list.  
4. Store the flattened list and maintain an index to track the current element.  
5. Implement `next()` to return the next integer and `hasNext()` to check if more integers exist.  
6. Test the iterator with a sample nested list.  
7. Stop the program.  

## Program:
```
/*
Program to find Flattening a Nested List Using an Iterator
Developed by: Sri Yaline R
RegisterNumber:  212224040325
*/

import java.util.*;
public class NestedIterator implements Iterator<Integer> {
    private List<Integer> integers = new ArrayList<>();
    private int position = 0;

    public NestedIterator(List<NestedInteger> nestedList) {
        flattenList(nestedList);
    }

    private void flattenList(List<NestedInteger> nestedList) {
        for(NestedInteger n:nestedList){
            if(n.isInteger()){
                integers.add(n.getInteger());
            }
            else{
                flattenList(n.getList());
            }
        }
    }

    @Override
    public Integer next() {
        return integers.get(position++);
        
    }
    @Override
    public boolean hasNext() {
       return position < integers.size();
        
    }
    public static List<NestedInteger> parse(String s) {
    Stack<List<NestedInteger>> stack = new Stack<>();
    List<NestedInteger> curr = new ArrayList<>();
    int num = 0;
    boolean hasNum = false;

    for (int i = 0; i < s.length(); i++) {
        char c = s.charAt(i);
        if (c == '[') {
            stack.push(curr);
            curr = new ArrayList<>();
        } else if (c == ']') {
            if (hasNum) {
                curr.add(new SimpleNestedInteger(num));
                hasNum = false;
                num = 0;
            }
            List<NestedInteger> completed = curr;
            curr = stack.pop();
            curr.add(new SimpleNestedInteger(completed));
        } else if (c == ',') {
            if (hasNum) {
                curr.add(new SimpleNestedInteger(num));
                hasNum = false;
                num = 0;
            }
        } else if (Character.isDigit(c)) {
            num = num * 10 + (c - '0');
            hasNum = true;
        }
    }
    return curr;
}


    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
      
        String input = sc.nextLine();

        List<NestedInteger> nestedList = parse(input);

        NestedIterator iterator = new NestedIterator(nestedList);
        List<Integer> output = new ArrayList<>();
        while (iterator.hasNext()) {
            output.add(iterator.next());
        }

        System.out.println(output);
    }
}

interface NestedInteger {
    boolean isInteger();
    Integer getInteger();
    List<NestedInteger> getList();
}

class SimpleNestedInteger implements NestedInteger {
    private Integer value;
    private List<NestedInteger> list;

    public SimpleNestedInteger(Integer value) {
        this.value = value;
        this.list = null;
    }

    public SimpleNestedInteger(List<NestedInteger> list) {
        this.list = list;
        this.value = null;
    }

    @Override
    public boolean isInteger() {
        return value != null;
    }

    @Override
    public Integer getInteger() {
        return value;
    }

    @Override
    public List<NestedInteger> getList() {
        return list;
    }
}
```

## Output:
<img width="844" height="156" alt="image" src="https://github.com/user-attachments/assets/85a4a368-82d4-419d-ac98-b5a2c5a22c21" />

## Result:
The JAVA program for NestedIterator class successfully flattens a nested list of integers into a single list and provides sequential access using standard iterator methods.
