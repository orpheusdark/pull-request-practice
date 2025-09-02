### **⚡ C++ Implementation (OOP Based)**

```cpp
#include <iostream>
#define SIZE 5 // Define the maximum size of the queue
using namespace std;

class Queue {
    int arr[SIZE]; // Array to hold queue elements
    int front, rear; // Pointers to track ends

public:
    // Constructor to initialize an empty queue
    Queue() {
        front = rear = -1; // -1 signifies the queue is empty
    }

    // Operation 1: Enqueue (Add an element to the end)
    void enqueue(int val) {
        // Check for Queue Overflow
        if ((rear + 1) % SIZE == front) {
            cout << "🚨 Queue Overflow! Can't add " << val << "." << endl;
            return;
        }
        // If the queue is empty, set front to 0
        if (front == -1) front = 0;
        // Move rear forward in a circular manner
        rear = (rear + 1) % SIZE;
        // Insert the new value at the new rear position
        arr[rear] = val;
        cout << "✅ Enqueued: " << val << endl;
    }

    // Operation 2: Dequeue (Remove an element from the front)
    void dequeue() {
        // Check for Queue Underflow
        if (front == -1) {
            cout << "🚨 Queue Underflow! Nothing to remove." << endl;
            return;
        }
        // Print the value being removed
        cout << "✅ Dequeued: " << arr[front] << endl;
        // If this was the last element, reset the queue to empty state
        if (front == rear)
            front = rear = -1;
        else // Otherwise, move front forward in a circular manner
            front = (front + 1) % SIZE;
    }

    // Operation 3: Traverse/Display (Print all elements from front to rear)
    void traverse() {
        if (front == -1) {
            cout << "📭 Queue is empty." << endl;
            return;
        }
        cout << "📋 Queue: ";
        int i = front;
        // Loop through the queue using a do-while to handle the circular nature
        while (true) {
            cout << arr[i] << " ";
            if (i == rear) break; // Stop after printing the rear element
            i = (i + 1) % SIZE; // Move to the next index circularly
        }
        cout << endl;
    }

    // Operation 4: Search (Find if an element exists in the queue)
    void search(int key) {
        if (front == -1) {
            cout << "📭 Queue is empty. Can't search." << endl;
            return;
        }
        int i = front;
        while (true) {
            if (arr[i] == key) {
                cout << "🔍 Element " << key << " found at index " << i << "." << endl;
                return;
            }
            if (i == rear) break;
            i = (i + 1) % SIZE;
        }
        cout << "🔍 Element " << key << " not found." << endl;
    }
};

int main() {
    cout << "🧪 Testing Queue Implementation (C++)" << endl;
    cout << "------------------------------------" << endl;
    Queue q; // Create a queue object

    q.traverse(); // Try to display empty queue

    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);
    q.enqueue(40);
    q.enqueue(50); // Queue should be full now
    q.enqueue(60); // This should cause overflow

    q.traverse();

    q.dequeue(); // Remove 10
    q.dequeue(); // Remove 20

    q.traverse(); // Should show [30, 40, 50]

    q.enqueue(60); // Should work now due to circular nature
    q.enqueue(70); // Should work

    q.traverse(); // Should show [30, 40, 50, 60, 70]

    q.search(40);
    q.search(99);

    return 0;
}
```

🧪 **Output**

```
📭 Queue is empty.
✅ Enqueued: 10
✅ Enqueued: 20
✅ Enqueued: 30
✅ Enqueued: 40
✅ Enqueued: 50
🚨 Queue Overflow! Can't add 60.
📋 Queue: 10 20 30 40 50 
✅ Dequeued: 10
✅ Dequeued: 20
📋 Queue: 30 40 50 
✅ Enqueued: 60
✅ Enqueued: 70
📋 Queue: 30 40 50 60 70 
🔍 Element 40 found at index 3.
🔍 Element 99 not found.
```
