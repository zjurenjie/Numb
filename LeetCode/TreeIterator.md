## 二叉树的三种遍历方式（递归和迭代）

#### 前序遍历

##### 递归

```java
public void preOrder(TreeNode root, List list) {
    if (root == null) {
        return;
    }
    
    list.add(root.val);
    preOrder(root.left, list);
    preOrder(root.right, list);
}
```

##### 迭代1

```java
public List preOrderIteration(TreeNode root) {
    List<Integer> list = new ArrayList<>();
    Deque<TreeNode> stack = new LinkedList<>();
    TreeNode node = root;
    while (node != null || !stack.isEmpty()) {
        while (node != null) {
            list.add(node.val);
            stack.push(node);
            node = node.left;
        }
        node = stack.pop();
        node = node.right;
    }
}
```



##### 迭代2

```java
public List preOrderIteration(TreeNode root) {
    List<Integer> list = new ArrayList<>();
    Deque<TreeNode> stack = new LinkedList<>();
    stack.push(root);
    while (!stack.isEmpty()) {
        TreeNode node = stack.pop();
        list.add(node.val);
        if (node.right != null) { // 栈是LIFO，所以先将右结点入栈，右结点后出栈
            stack.push(node.right);
        }
        if (node.left != null) {
            stack.push(node.left);
        }
    }
    return list;
    
}
```

#### 中序遍历

##### 递归

```java
public void inOrder(TreeNode root, List list) {
    if (root == null) {
        return;
    }
    inOrder(root.left, list);
    list.add(root.val);
    inOrder(root.right, list);
}
```

##### 迭代

```java
public List inOrder(TreeNode root) {
    Deque<TreeNode> stack = new LinkedList<>();
    List<Integer> list = new ArrayList<>();
    TreeNode node = root;
    while (node != null || !stack.isEmpty()) {
        while (node != null) { // 一直往下寻找直到最左的结点
            stack.push(node);
            node = node.left;
        }
        node = stack.pop(); // 取出栈底元素 
        list.add(node.val);
        node = node.right(); // 尝试添加右结点入栈
    }
    return list;
}
```

#### 后序遍历

##### 递归

```java
public void posOrder(TreeNode root, List list) {
    if (root == null) {
        return;
    }
    posOrder(root.left, list);
    posOrder(root.right, list);
    list.add(root.val);
}
```

##### 迭代

```java
public List posOrderIteration(TreeNode root) {
    Deque<TreeNode> stack = new LinkedList<>();
    List<Integer> list = new ArrayList<>();
    TreeNode node = root;
    TreeNode pre = null;
    while (node != null || !stack.isEmpty()) {
        while (node != null) {
            stack.push(node);
            node = node.left;
        }
        node = stack.peek();
        if (node.right == null || node.right == null) {
            pre = root;
            list.add(stack.pop().val);
            node = null;
        }
    } 
 }
```

