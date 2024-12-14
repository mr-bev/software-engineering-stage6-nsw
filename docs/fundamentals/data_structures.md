# Data Structures

In all cases you should not need to implement these data structures yourself. Use the built in version for the language or use a library. The code below is provided to illustrate how these data structures are implemented. The cose is valid and you could use it to debug or step through code to get a better understanding of them.

## Array

## Multi-dimensional Array

## List :material-school:

A list is a sequence optimised for insertion and deletion of elements. A list is dynamic in size unlike and array that is of fixed size. Lists can grow and shrink as needed meaning they will be memory efficient although there is some overhead in maintaining the reference to the next and previous item. Lists are not ordered unless specifically made to be ordered and can have duplicate values. They are accessed sequentially both forward and backward although going backward is slower for a single linked list as you can only iterated over the list front the front. Random access is slower than other data structures.

!!! note
    Every programming language has its own features when it comes to lists. Eg: C++ doesn't offer an index operator due to its definition in the language. 

| Action | Parameters | Description | [Performance](./big_o.md) |
| :----: | :--------: | :---------: | :---------: |
| Insert |  value     | Add the value to the end of the list | O(1) |
| Access |  index     | Fetch the value from the indexed location in the list | O(n) |
| Search |  value     | Find the value in the list | Worst case O(n), Average case O(n/2), Best case O(1) |
| Delete |  value     | Remove the value from the list. This can be language specific, some will remove only the first item found, others will remove all. Others will consider a delete being from the head or tail of the list only. | Worst case O(n), Average case O(n/2), Best case O(1) |

### Single Linked List

Not commonly used, it is called a single linked list as it links in a single direction from the head to the next item in the list.
![Single Link List](./images/single-linked-list.png)


### Double Linked List

Double linked as it has references in both directions to traverse a list. This does use more memory that a single linked list but does improve significantly it usage. With this stucture in place it can also be used as the basis for a stack, queue and deque (pronouced deck).

![Double Linked List](./images/double-linked-list.png)

??? code

    === "Python"

        ``` py
        class Node:
            def __init__(self, data):
                self.item = data
                self.next: Node = None
                self.prev: Node = None

            def __repr__(self):
                return f'Node: {self.item}'

        class LinkedList:
            def __init__(self):
                self.head: Node = None
                self.tail: Node = None

            def add(self, data):
                node = Node(data)
                if self.tail != None:
                    node.prev = self.tail
                    self.tail.next = node
                self.tail = node
                
                if self.head == None:
                    self.head = node
                
            def find(self, data) -> bool:
                node = self.head
                while node != None and data != node.item:
                    node = node.next
                
                return node != None
            
            def remove(self, data) -> bool:
                if self.head == None:
                    return False

                node = self.head
                while data != node.item:
                    node = node.next

                if node == None:
                    return False

                # only 1 node in the list
                if node.prev == None and node.next == None:
                    self.head = None
                    self.tail = None
                    return True
                
                # last node in the list
                if node.next == None:
                    node.prev.next = None
                    self.tail = node.prev
                    node.prev = None
                # first node in the list
                elif node.prev == None:
                    node.next.prev = None
                    self.head = node.next
                    node.next = None
                # node is in the middle of the list
                else:
                    node.prev.next = node.next
                    node.next.prev = node.prev
                    node.next = None
                    node.prev = None
                
                return True

            def __repr__(self):
                output = 'LinkedList: '
                node = self.head
                while node != None:
                    output += f'({node}), '
                    node = node.next
                
                return output
        ```

    === "C#"



    === "Rust" 


### Ordered List

## Stack

## Queue

## Deque

## Hashmap

## Dictionary

## Trees