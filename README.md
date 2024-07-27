import java.util.Scanner;

class Node {
    int data;
    Node next;

    Node(int d) {
        data = d;
        next = null;
    }
}

class LinkedList {
    Node head;

    public LinkedList() {
        head = null;
    }

    // Function to insert a node at the end of the linked list
    public void insert(int data) {
        Node newNode = new Node(data);
        if (head == null) {
            head = newNode;
        } else {
            Node temp = head;
            while (temp.next != null) {
                temp = temp.next;
            }
            temp.next = newNode;
        }
    }

    // Function to print the linked list
    public void printList() {
        Node temp = head;
        while (temp != null) {
            System.out.print(temp.data + " ");
            temp = temp.next;
        }
    }
}

public class Main {
    public static Node mergeLists(Node l1, Node l2) {
        if (l1 == null)
            return l2;
        if (l2 == null)
            return l1;

        Node mergedList;

        if (l1.data <= l2.data) {
            mergedList = l1;
            mergedList.next = mergeLists(l1.next, l2);
        } else {
            mergedList = l2;
            mergedList.next = mergeLists(l1, l2.next);
        }

        return mergedList;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int T = scanner.nextInt();

        for (int t = 0; t < T; t++) {
            int N1 = scanner.nextInt();
            LinkedList list1 = new LinkedList();
            for (int i = 0; i < N1; i++) {
                list1.insert(scanner.nextInt());
            }

            int N2 = scanner.nextInt();
            LinkedList list2 = new LinkedList();
            for (int i = 0; i < N2; i++) {
                list2.insert(scanner.nextInt());
            }

            Node mergedList = mergeLists(list1.head, list2.head);
            LinkedList mergedLinkedList = new LinkedList();
            mergedLinkedList.head = mergedList;

            mergedLinkedList.printList();
            System.out.println();
        }

        scanner.close();
    }
}
