# LeetCode-Solutions-For-Linked-List-Cycle

## Original question
>Given `head`, the head of a linked list, determine if the linked list has a cycle in it.
>
>There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the `next` pointer. Internally, `pos` is used to denote the index of the node that tail's `next` pointer is connected to. **Note that `pos` is not passed as a parameter.**
>
>Return `true` if there is a cycle in the linked list. Otherwise, return `false`.
>
>Example 1:
>![image](https://user-images.githubusercontent.com/90940182/166614275-5163bcf9-e5ee-48ed-af36-e5d71aff84f5.png)
>
>Input: head = [3,2,0,-4], pos = 1
>
>Output: true
>
>Explanation: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).

>Example 2:
>![image](https://user-images.githubusercontent.com/90940182/166614385-850b55b6-bfd9-4577-8eb0-1e86f9f0e8e5.png)
>
>Input: head = [1,2], pos = 0
>
>Output: true
>
>Explanation: There is a cycle in the linked list, where the tail connects to the 0th node.

>Example 3:
>![image](https://user-images.githubusercontent.com/90940182/166614427-c5a1a47b-4d3a-4d6b-a8b8-34f04f32be9a.png)
>
>Input: head = [1], pos = -1
>
>Output: false
>
>Explanation: There is no cycle in the linked list.

## Solution Explanation

If the linked list has a cycle in it, the pointer will never reach the end of the list, which is `NULL`.

Given two pointers pointing to the head, one is called a fast pointer, and one is called a slow pointer. 

Every time they move, the fast pointer will move two points forward, and the slow pointer will move one point forward. 

If the list has a cycle in it, the fast and slow pointer will eventually equal. Which is `slow == fast`.


    bool hasCycle(struct ListNode *head) {
    
    struct ListNode * fast = head, *slow = head;
    
    while(fast&&fast->next)
    
    {
    
        fast = fast->next->next;
        
        slow = slow->next;
        
        if(fast == slow)
        
        {
        
            return true;
            
        }
        
    }
    
    return false;
    


## Further Questions

### Why does the slow pointer go one step forward, and the fast pointer goes two steps forward, and they will meet in the cycle? Is there any possibility that fast will never meet slow? Prove it.


These two pointers will eventually meet if the list has a cycle in it.

Suppose when the slow pointer gets into the circle, the distance between two pointers is **_N_**.

While the fast pointer is chasing the slow pointer, every time the fast pointer moves two steps forward, the slow pointer moves one step forward.
The distance between those two pointers will be:
N

N-1

N-2

N-3

……

…

1

0

Since the distance will eventually equal zero, no matter how large is the cycle or how small is the cycle, those two pointers will meet in the list if the list has a cycle. 

Figure explanation for the fast and slow pointer:
![7be0199ec73a63606f4b5d63c1a7b5b](https://user-images.githubusercontent.com/90940182/166616293-e5c40cfc-1c60-4dde-a0c1-9d791992c4b9.jpg)


### If the slow pointer moves one step forwards every time, but the fast pointer moves three steps forwards, will they meet in the cycle? How about every time the fast pointer moves four steps forwards? _x_ steps forwards? Prove it.

No, those two pointers will not definitely meet in the cycle.

Suppose when the slow pointer gets into the circle, the distance between two pointers is **_N_**.

While the fast pointer is chasing the slow pointer, every time the fast pointer moves three steps forward, the slow pointer moves one step forward.
The distance between those two pointers will be:

Suppose **_N_** is even: 

N

N-2

N-4

N-6

……

…

2

0

If the distance **_N_** between those two pointers is even, they will meet in the cycle. 

However, consider the following situation:

Suppose **_N_** is odd: 

N

N-2

N-4

N-6

……

…

1

-1

The distance between two pointers will be -1, which is the total distance of the cycle minus 1. 

Suppose the total distance of the Cycle is C, and C is even.

The distance between two pointers will be:

C-1

C-3

C-5

……

…

3

1

-1  == C-1

C-3

 
Then, this loop becomes an infinite loop. And these two pointers will never meet in the cycle.


It will be the same when the fast pointer is moving four steps forwards or x steps forwards.


Figure explanation for the fast and slow pointer:
![5a294325ed2d129985bfc4a4642b95b](https://user-images.githubusercontent.com/90940182/166618109-fd61d46a-4e1c-482a-8769-2508abdbf6d9.jpg)


