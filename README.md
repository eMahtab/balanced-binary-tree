# Balanced Binary Tree
## https://leetcode.com/problems/balanced-binary-tree

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:

    a binary tree in which the left and right subtrees of every node differ in height by no more than 1.

 
```
Example 1:

Given the following tree [3,9,20,null,null,15,7]:

    3
   / \
  9  20
    /  \
   15   7

Return true.

Example 2:

Given the following tree [1,2,2,3,3,null,null,4,4]:

       1
      / \
     2   2
    / \
   3   3
  / \
 4   4

Return false.
```

## Implementation :

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    private static class BalanceStatusWithHeight {
      public boolean isBalanced;
      public int height;

      public BalanceStatusWithHeight(boolean isBalanced, int height) {
        this.isBalanced = isBalanced;
        this.height = height;
      }
    }

    public boolean isBalanced(TreeNode root) {
      return checkBalanced(root).isBalanced;
    }

    private static BalanceStatusWithHeight checkBalanced(TreeNode root) {

      // Base case, an empty subtree is balanced and has a height of -1
      if (root == null) {
        return new BalanceStatusWithHeight(true, -1);
      }

     //  Go deep into the left subtree and get a result back
     BalanceStatusWithHeight leftResult = checkBalanced(root.left);
     if (!leftResult.isBalanced) {
       return leftResult; // Left subtree is not balanced. Bubble up failure.
     }

     // Go deep into the right subtree and get a result back
     BalanceStatusWithHeight rightResult = checkBalanced(root.right);
     if (!rightResult.isBalanced) {
      return rightResult; // Right subtree is not balanced. Bubble up failure.
    }
    
    boolean subtreesAreBalanced = Math.abs(leftResult.height - rightResult.height) <= 1;
    int height = Math.max(leftResult.height, rightResult.height) + 1;

    return new BalanceStatusWithHeight(subtreesAreBalanced, height);
  }
}


```


# References :
https://www.youtube.com/watch?v=LU4fGD-fgJQ
