# 剑指offer 1-5

## 1.在一个二维数组中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数

``` java
class Solution {
    public boolean Find(int target, int [][] array){
        int rows = array.length;
        if(rows == 0){
            return false;
        }
        int cols = array[0].length;
        if(cols == 0){
            return false;
        }
        int row = 0;
        int col = cols -1;
        while(row < rows && col >= 0){
            if(array[row][col] < target){
                row++;
            }else if (array[row][col] > target){
                col--;
            }else {
                return true;
            }
        }
        return false;
    }
}
```

## 2.请实现一个函数，将一个字符串中的每个空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy

``` java
public class Solution {
    public String replaceSpace(StringBuffer str) {
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < str.length(); i++) {
            if (str.charAt(i) == ' ') {
                sb.append("%20");
            } else {
                sb.append(str.charAt(i));
            }
        }
        return sb.toString();
    }
}
```

## 3.输入一个链表，按链表从尾到头的顺序返回一个ArrayList

``` java
import java.util.ArrayList;
import java.util.Stack;

public class Solution {
    public class ListNode {
        int val;
        ListNode next = null;
        ListNode(int val) {
            this.val = val;
        }
    }

    public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
        ArrayList<Integer> list = new ArrayList<>();
        Stack<Integer> stack = new Stack<>();
        while (listNode != null){
            stack.push(listNode.val);
            listNode = listNode.next;
        }
        while (!stack.isEmpty()){
            list.add(stack.pop());
        }
        return list;
    }
}
```

## 4.输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回

``` java
import java.util.Arrays;

public class Solution {
    private class TreeNode {
        int val;
        public TreeNode(int v) {
            val = v;
        }
        TreeNode leftNode;
        TreeNode rightNode;
    }

    public TreeNode reConstructBinaryTree(int[] pre, int[] in) {
        if (pre.length == 0 || in.length == 0) {
            return null;
        }
        int pre0 = pre[0];
        TreeNode tn = new TreeNode(pre0);
        for (int i = 0; i < in.length; i++) {
            if (in[i] == pre0) {
                tn.leftNode = reConstructBinaryTree(Arrays.copyOfRange(pre, 1, i + 1), Arrays.copyOfRange(in, 0, i));
                tn.rightNode = reConstructBinaryTree(Arrays.copyOfRange(pre, i + 1, pre.length), Arrays.copyOfRange(in, i + 1, in.length));
                break;
            }
        }
        return tn;
    }
}
```

## 5.用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型

``` java
import java.util.Stack;

public class Solution {
    Stack<Integer> stack1 = new Stack<Integer>();
    Stack<Integer> stack2 = new Stack<Integer>();

    public void push(int node) {
        stack1.push(node);
    }

    public int pop() {
        if (stack2.isEmpty()) {
            while (!stack1.isEmpty()) {
                stack2.push(stack1.pop());
            }
        }
        return stack2.pop();
    }
}
```
