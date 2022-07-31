# Queue

Now that we have already learned what a linked list is, it should be easy to quickly setup a queue.

A queue is a data structure that implements the FIFO (first in first out) principle.

What that means is that when you add data to the queue, it is added to data structure like a queue, as in it is **added to the back of the line**.

When you remove data from the queue, we take data **from the front of the line**.


## Example of a queue
We have a queue:

1|4|6|8
---|---|---|---

So when we add `3` to the queue, we get:
3|1|4|6|8
---|---|---|---|---

and when we try to remove from the queue, it becomes
3|1|4|6
---|---|---|---

and returns `8`.


## Implementation (C)
Bored of the details yet? Let's implement our queue.

And while we're at it, let's copy our linked list too.

```cpp
struct Element {
    int data;
    Element *next;
};

struct Queue {
    int size;
    Element *front;
    Element *back;

    Queue() {
        size = 0;
        front = nullptr;
        back = nullptr;
    }
};
```

Literally single linked list with a different name.

Btw, the `*` after a typename means that it is a pointer, and `nullptr` stands for `Null Pointer`.

Now let's implement the `enqueue` function.

```cpp
struct Queue {
    // --snip--

    void enqueue(int data) {
        // Create a new temporary element.
        Element *tmp = new Element;
        
        // Set the data of the new element.
        tmp->data = data;
        tmp->next = nullptr;

        // If the queue is empty, set the front and back to the new element.
        if (front == nullptr) {
            front = tmp;
            back = tmp;
        } else {
            // Otherwise, set the next element of the back to the new element.
            back->next = tmp;
            // And set the back to the new element.
            back = tmp;
        }

        // Increment the size of the queue.
        size++;
    }
}
```

Oof, that's a lot of code, isn't it? Hope you don't mind, the explanations are in the comments.

Next, let's implement the `dequeue` function.

```cpp
#include <limits>

struct Queue {
    // --snip--

    int dequeue() {
        // If the queue is empty, return the minimum integer.
        // Typically you wouldn't have to deal with INT_MIN,
        // so it's a perfect candidate for the sentinel value.
        if (front == nullptr) {
            return INT_MIN;
        }
        
        // Create a temporary element.
        Element *tmp = front;
        
        // Set the front to the next element.
        front = front->next;
        
        // Decrement the size of the queue.
        size--;
        
        // Return the data of the temporary element.
        return tmp->data;
    }
}
```

And there we go. We got a working queue by just adding two functions to a linked list data structure. Amazing!

As a practice challenge, try to implement a `print` function for the queue.

See ya!