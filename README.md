# binary search tree implementation in java 
# Binary Search Tree (BST)

    A binary search tree is a special kind of [binary tree](../Binary%20Tree/) (a tree in which each node has at most two children) that performs insertions and deletions such that the tree is always sorted.


## "Always sorted" property

    Here is an example of a valid binary search tree:

![A binary search tree](Images/Tree1.png)

    Notice how each left child is smaller than its parent node, and each right child is greater than its parent node. This is the key feature of a binary search tree.

    For example, `2` is smaller than `7`, so it goes on the left; `5` is greater than `2`, so it goes on the right.

## Inserting new nodes

    When performing an insertion, we first compare the new value to the root node. If the new value is smaller, we take the *left* branch; if greater, we take the *right* branch. We work our way down the tree this way until we find an empty spot where we can insert the new value.

    Suppose we want to insert the new value `9`:

    - We start at the root of the tree (the node with the value `7`) and compare it to the new value `9`.
    - `9 > 7`, so we go down the right branch and repeat the same procedure but this time on node `10`.
    - Because `9 < 10`, we go down the left branch.
    - We now arrived at a point where there are no more values to compare with. A new node for `9` is inserted at that location.

    Here is the tree after inserting the new value `9`:

![After adding 9](Images/Tree2.png)

    There is only one possible place where the new element can be inserted in the tree. Finding this place is usually quick. It takes **O(h)** time, where **h** is the height of the tree.

> **Note:** The *height* of a node is the number of steps it takes to go from that node to its lowest leaf. The height of the entire tree is the distance from the root to the lowest leaf. Many of the operations on a binary search tree are expressed in terms of the tree's height.

By following this simple rule -- smaller values on the left, larger values on the right -- we keep the tree sorted, so whenever we query it, we can check if a value is in the tree.

## Searching the tree

    To find a value in the tree, we perform the same steps as with insertion:

    - If the value is less than the current node, then take the left branch.
    - If the value is greater than the current node, take the right branch.
    - If the value is equal to the current node, we've found it!

    Like most tree operations, this is performed recursively until either we find what we are looking for or run out of nodes to look at.

    Here is an example for searching the value `5`:

![Searching the tree](Images/Searching.png)

Searching is fast using the structure of the tree. It runs in **O(h)** time. If you have a well-balanced tree with a million nodes, it only takes about 20 steps to find anything in this tree. (The idea is very similar to [binary search](../Binary%20Search) in an array.)

## Traversing the tree

Sometimes you need to look at all nodes rather than only one.

There are three ways to traverse a binary tree:

1. *In-order* (or *depth-first*): first look at the left child of a node then at the node itself and finally at its right child.
2. *Pre-order*: first look at a node then its left and right children.
3. *Post-order*: first look at the left and right children and process the node itself last.

Traversing the tree also happens recursively.

If you traverse a binary search tree in-order, it looks at all the nodes as if they were sorted from low to high. For the example tree, it would print `1, 2, 5, 7, 9, 10`:

![Traversing the tree](Images/Traversing.png)

## Deleting nodes

Removing nodes is easy. After removing a node, we replace the node with either its biggest child on the left or its smallest child on the right. That way the tree is still sorted after the removal. In the following example, 10 is removed and replaced with either 9 (Figure 2) or 11 (Figure 3).

![Deleting a node with two children](Images/DeleteTwoChildren.png)

Note the replacement needs to happen when the node has at least one child. If it has no child, you just disconnect it from its parent:

![Deleting a leaf node](Images/DeleteLeaf.png)
# The code (solution 1)

So much for the theory. Let's see how we can implement a binary search tree in Java. There are different approaches you can take. First, I will show you how to make a class-based version, but we will also look at how to make one using enums.

Here is an example for a `BinarySearchTree` class:

