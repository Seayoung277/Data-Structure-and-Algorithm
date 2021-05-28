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
    - max(Left) <= Root.val <= min(Right)

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
- Iterative (with stack)
```
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        
        while (root != null || !stack.empty()) {
            while (root != null) {
                stack.push(root);
                root = root.left;
            }
            root = stack.pop();
            result.add(root.val);
            root = root.right;
        }
        
        return result;
    }
}
```
- Morris (without stack)
```
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        TreeNode tmp;
        
        while (root != null) {
            if (root.left == null) {
                result.add(root.val);
                root = root.right;
            }
            else {
                tmp = root.left;
                while (tmp.right != null && tmp.right != root) {
                    tmp = tmp.right;
                }
                if (tmp.right == null) {
                    tmp.right = root;
                    root = root.left;
                } else {
                    result.add(root.val);
                    tmp.right = null;
                    root = root.right;
                }
            }
        }
        
        return result;
    }
}
```

### Preorder Traversal

#### Definition
- Root -> Left -> Right

#### LeetCode
[144. Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/)

#### Implementations
- Recursive
```
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList();
        traverse(root, result);
        return result;
    }
    
    private void traverse(TreeNode root, List<Integer> result) {
        if (root == null) return;
        
        result.add(root.val);
        traverse(root.left, result);
        traverse(root.right, result);
    }
}
```
- Iterative (with stack)
```
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        
        while (root != null || !stack.empty()) {
            while (root != null) {
                result.add(root.val);
                stack.push(root.right);
                root = root.left;
            }
            root = stack.pop();
        }
        
        return result;
    }
}
```
- Morris (without stack)
```
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new LinkedList<>();
        TreeNode tmp;
        
        while (root != null) {
            if (root.left == null) {
                result.add(root.val);
                root = root.right;
            }
            else {
                tmp = root.left;
                while (tmp.right != null && tmp.right != root) {
                    tmp = tmp.right;
                }
                if (tmp.right == null) {
                    result.add(root.val);
                    tmp.right = root;
                    root = root.left;
                } else {
                    tmp.right = null;
                    root = root.right;
                }
            }
        }
        
        return result;
    }
}
```

### Postorder Traversal

#### Definition
- Left -> Right -> Root

#### LeetCode
[145. Binary Tree Postorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal/)

#### Implementations
- Recursive
```
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList();
        traverse(root, result);
        return result;
    }
    
    private void traverse(TreeNode root, List<Integer> result) {
        if (root == null) return;
        
        traverse(root.left, result);
        traverse(root.right, result);
        result.add(root.val);
    }
}
```
- Double Stack (Preorder and reverse)
```
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList();
        Stack<TreeNode> stack = new Stack();
        
        while (root != null || !stack.empty()) {
            while (root != null) {
                result.add(root.val);
                stack.push(root.left);
                root = root.right;
            }
            root = stack.pop();
        }
        
        Collections.reverse(result);
        return result;
    }
}
```
- Single Stack (Keep record of Prev)
```
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList();
        Stack<TreeNode> stack = new Stack();
        TreeNode prev = root;
        
        stack.push(root);
        while (!stack.empty()) {
            root = stack.peek();
            if (root == null) {
                prev = stack.pop();
            }
            else if (root.left == null && root.right == null || prev == root.right) {
                result.add(root.val);
                prev = stack.pop();
            } else if (prev == root.left) {
                prev = root;
                stack.push(root.right);
            } else {
                prev = root;
                stack.push(root.left);
            }
        }
        
        return result;
    }
}
```