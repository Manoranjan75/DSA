#  Implement Queue using Array (C++)

---

##  Problem Statement

Design a basic **Queue** data structure using an **array**.

The Queue should support these operations:

1. `enqueue(x)` — Insert element `x` at the end (rear) of the queue.  
2. `dequeue()` — Remove the element from the front of the queue.  
3. `frontElement()` — Get the element at the front.  
4. `isEmpty()` — Check if the queue is empty.  
5. `isFull()` — Check if the queue is full.  
6. `display()` — Print the current queue elements.

---

##  Example

### Input:
```cpp
enqueue(10)
enqueue(20)
enqueue(30)
dequeue()
enqueue(40)
display()

output:
Queue elements: 20 30 40
Front: 20
Rear: 40

#include <bits/stdc++.h>
using namespace std;

class Queue {
    int *arr;
    int size;
    int front, rear;

public:
    Queue(int n) {
        size = n;
        arr = new int[size];
        front = -1;
        rear = -1;
    }

    // Enqueue: insert element at rear
    void enqueue(int val) {
        if (rear == size - 1) {
            cout << "Queue Overflow!" << endl;
            return;
        }

        if (front == -1) front = 0;
        arr[++rear] = val;
        cout << val << " enqueued!" << endl;
    }

    // Dequeue: remove element from front
    void dequeue() {
        if (front == -1 || front > rear) {
            cout << "Queue Underflow!" << endl;
            return;
        }

        cout << arr[front] << " dequeued!" << endl;
        front++;
    }

    // Get the front element
    int frontElement() {
        if (front == -1 || front > rear) {
            cout << "Queue is empty!" << endl;
            return -1;
        }
        return arr[front];
    }

    // Check if empty
    bool isEmpty() {
        return (front == -1 || front > rear);
    }

    // Check if full
    bool isFull() {
        return (rear == size - 1);
    }

    // Display the queue
    void display() {
        if (front == -1 || front > rear) {
            cout << "Queue is empty!" << endl;
            return;
        }

        cout << "Queue elements: ";
        for (int i = front; i <= rear; i++) {
            cout << arr[i] << " ";
        }
        cout << endl;
    }

    ~Queue() {
        delete[] arr;
    }
};

int main() {
    Queue q(5);

    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);
    q.dequeue();
    q.enqueue(40);

    q.display();

    cout << "Front element: " << q.frontElement() << endl;
    cout << "Is queue full? " << (q.isFull() ? "Yes" : "No") << endl;
    cout << "Is queue empty? " << (q.isEmpty() ? "Yes" : "No") << endl;

    return 0;
}

