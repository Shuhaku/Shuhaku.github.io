---
title: '[Algorithm] Tortoise and Hare'
date: 2024-12-29 12:00:00 +0000
categories: [Algorithm]
tags: [Algorithm]
author: Shuhaku
mermaid: true
---

> This post may contain errors.  
> Please use it for reference only.
{: .prompt-warning }

## Development Environment

* M1 Macbook
* Docker version 24.0.2

```java

class ListNode {
  int val;
  ListNode next;
  ListNode(int x) {
    val = x;
    next = null;
  }
}

```

Below is the implementation of a method to check if a singly linked list contains a cycle:

```java
public boolean hasCycle(ListNode head) {
    if (head == null || head.next == null) {
        return false;
    }

    ListNode oneStep = head;
    ListNode twoStep = head;

    while (twoStep != null && twoStep.next != null) {
        oneStep = oneStep.next;
        twoStep = twoStep.next.next;

        if (oneStep == twoStep) {
            return true;
        }
    }

    return false;
}
```

- oneStep moves one node at a time.
- twoStep moves two nodes at a time.
- If the linked list has a cycle, **oneStep** and **twoStep** will eventually meet.
  → Reason: Since the two pointers move at different speeds, they will eventually overlap while traversing the cycle.
- If there is no cycle, **twoStep** will reach the end of the list (i.e., null).

```java
    public static ListNode findCycleStart(ListNode head) {
        ListNode oneStep = head;
        ListNode twoStep = head;

        while (twoStep != null && twoStep.next != null) {
            oneStep = oneStep.next;
            twoStep = twoStep.next.next;

            if (oneStep == twoStep) {
                oneStep = head; 
                while (oneStep != twoStep) {
                    oneStep = oneStep.next;
                    twoStep = twoStep.next;
                }
                return oneStep;
            }
        }

        return null;
    }
```

This approach is efficient, using O(n) time complexity and O(1) space complexity.

