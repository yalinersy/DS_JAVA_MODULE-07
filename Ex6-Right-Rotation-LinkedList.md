# Ex6 Right Rotation LinkedList
## DATE: 26.1.26
## AIM:
To write a Java  program to:
Create a singly linked list.
Rotate the linked list to the right by k positions.
Display the rotated linked list.
## Algorithm
1. Start the program and read the number of nodes n and their data values.
2. Create a singly linked list by linking each new node to the previous one.
3. Traverse the linked list to find its length and connect the last node to the head, forming a circular list.
4. Calculate the effective rotation using k = k % length, then move (length - k) steps to find the new head and tail nodes.
5. Break the circular link by setting the new tail’s next to null, then display the rotated linked list.   

## Program:
```
/*
Program to  Right Rotation LinkedList
Developed by: Sri Yaline R
RegisterNumber:  212224040325
*/

import java.util.Scanner;
public class RotateLinkedList {
        public static Node rotate(Node head, int k) {
    if (head == null || head.next == null || k == 0) {
        return head;
    }
    Node current = head;
    int length = 1;
    while (current.next != null) {
        current = current.next;
        length++;
    }
    current.next = head;
    k = k % length;
    int stepsToNewTail = length - k;
    Node newTail = current = head;
    for (int i = 1; i < stepsToNewTail; i++) {
        current = current.next;
    }
    Node newHead = current.next;
    current.next = null;
    return newHead;
    }
    public static void display(Node head) {
        Node current = head;
        System.out.print("LinkedList: ");
        while (current != null) {
            System.out.print(current.data + " ");
            current = current.next;
        }
        System.out.println();
    }
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Node head = null, tail = null;
        int n = scanner.nextInt();
        for (int i = 0; i < n; i++) {
            Node newNode = new Node(scanner.nextInt());
            if (head == null) {
                head = tail = newNode;
            } else {
                tail.next = newNode;
                tail = newNode;
            }
        }
        int k = scanner.nextInt();
        head = rotate(head, k);
        display(head);
        scanner.close();
    }
}
class Node {
    int data;
    Node next;
    Node(int data) {
        this.data = data;
        this.next = null;
    }
}
```
## Output:
<img width="847" height="205" alt="image" src="https://github.com/user-attachments/assets/c6dd93a4-1a9f-4239-9232-80b74495924b" />



## Result:
Thus, the JAVA program to perfom right rotation on linked list is implemented successfully.
