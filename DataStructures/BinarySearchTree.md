# Binary Search Tree (BST)

## Basic Concepts of Tree

- Root and Leaf
- Parent, Child and Sibling
- Degree, Depth and Height
- Subtree and Forest

## Binary Tree

- Each node has no more than 2 children
- Full Binary Tree
    - each node has 0 or 2 children
- Complete Binary Tree
    - all levels are filled except bottom level
- Binary Search Tree
    - max(LEFT) <= root.val <= min(RIGHT)

## Binary Tree Traversal

### Levelorder Traversal

#### Definition
- Traverse by level, from top to bottom


### Inorder Traversal

#### Definition
- Left -> Root -> Right

#### LeetCode
[94. Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)

#### Implementations
- Recursive
```
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList();
        traverse(root, result);
        return result;
    }
    
    private void traverse(TreeNode root, List<Integer> result) {
        if (root == null) return;
        
        traverse(root.left, result);
        result.add(root.val);
        traverse(root.right, result);
    }
}
```

### Preorder Traversal

#### Definition
- Root -> Left -> Right


### Postorder Traversal

#### Definition
- Left -> Right -> Root