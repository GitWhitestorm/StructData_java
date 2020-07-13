# StructData_java
## 树



### 堆树

#### 定义

- 堆是一种**非线性结构**可以把堆看作一个数组，也可以被看作一个完全二叉树，通俗来讲**堆其实就是利用完全二叉树的结构来维护的一维数组**
- 按照堆的特点可以把堆分为**大顶堆**和**小顶堆**
- 大顶堆：每个结点的值都**大于**或**等于**其左右孩子结点的值(本片以大顶堆为例)
- 小顶堆：每个结点的值都**小于**或**等于**其左右孩子结点的值
- 堆排序：每次取出堆顶元素再重新排成堆

#### 结构设计

- 节点

  ``` java
  class Node{
      private int key;
      public Node(int initKey){
          key = initKey;
      }
      public int getKey(){
          return key;
      }
  }
  ```

- 数组

  ``` java
   private Node[] heapArray;
  ```
  
  

| Index | 0    | 1    | 2    | 3    | 4    |  5   | 6    |
| :---- | :--- | ---- | ---- | ---- | ---- | :--: | ---- |
| key   | 78   | 33   | 57   | 7    | 9    |  31  | 47   |

![大顶堆](/Users/whitestorm/Downloads/IMG_99C7A9C0636F-1.jpeg)

**index对应：leftchild = （parent-1）/2;rightchild = leftchild+1**

####  功能设计 ——insert

```java
//插入 向上检索
  public boolean insert(int key){
        if (currSize == maxSize)
        {
            return false;
        }
        Node node = new Node(key);
        heapArray[currSize] = node;
        trickleUp(currSize++);
    //	可改写为
    //	trickleUp(currSize);
    //	currSize++;
        return true;
    }
    public void trickleUp(int i){
        int parent = (i-1)/2;
        Node temp = heapArray[i];
        while (i>0 && heapArray[i].getKey()>heapArray[parent].getKey()){
            heapArray[i] = heapArray[parent];
            i = parent;
            parent = (i-1)/2;
        }
        heapArray[i] = temp;
    }

```

#### 功能设计—— delete

```java
// 取出MaxNum 向下检索
public Node delete(){
        Node root = heapArray[0];
        heapArray[0] = heapArray[--currSize];
        trickleDown(0);
        return root;
    }
    private void trickleDown(int i){
        int largeChild;//记录左右孩子最大值的下标
        Node top = heapArray[i];
        while (i< currSize/2){
            int leftChild = i*2+1;
            int rightChild = leftChild+1;
            if(rightChild < currSize && heapArray[rightChild].getKey() >
                    heapArray[leftChild].getKey()) {
                largeChild = rightChild;
            } else {
                largeChild = leftChild;
            }
            if(top.getKey() >= heapArray[largeChild].getKey())
            {
                break;
            }
            heapArray[i] = heapArray[largeChild];
            i = largeChild;

        }
        heapArray[i] = top;
    }
}
```

#### 完整源码

``` java

/**
 * @author whiteStorm
 * @date 2020/7/8
 */
public class TreeHeap {
    private Node[] heapArray;
    private int maxSize;
    private int currSize;
    public TreeHeap(int size){
     maxSize = size;
     currSize = 0;
     heapArray = new Node[size];
    }
    public boolean isEmpty(){
        return (currSize == 0);
    }
    public boolean insert(int key){
        if (currSize == maxSize)
        {
            return false;
        }
        Node node = new Node(key);
        heapArray[currSize] = node;
        trickleUp(currSize++);
        return true;
    }
    public void trickleUp(int i){
        int parent = (i-1)/2;
        Node temp = heapArray[i];
        while (i>0 && heapArray[i].getKey()>heapArray[parent].getKey()){
            heapArray[i] = heapArray[parent];
            i = parent;
            parent = (i-1)/2;
        }
        heapArray[i] = temp;
    }
    public Node delete(){
        Node root = heapArray[0];
        heapArray[0] = heapArray[--currSize];
        trickleDown(0);
        return root;
    }
    private void trickleDown(int i){
        int largeChild;
        Node top = heapArray[i];
        while (i< currSize/2){
            int leftChild = i*2+1;
            int rightChild = leftChild+1;
            if(rightChild < currSize && heapArray[rightChild].getKey() >
                    heapArray[leftChild].getKey()) {
                largeChild = rightChild;
            } else {
                largeChild = leftChild;
            }
            if(top.getKey() >= heapArray[largeChild].getKey())
            {
                break;
            }
            heapArray[i] = heapArray[largeChild];
            i = largeChild;

        }
        heapArray[i] = top;
    }
}
class Node{
    private int key;
    public Node(int initKey){
        key = initKey;
    }
    public int getKey(){
        return key;
    }
}

```

### 二叉搜索树

#### 定义

- 若任意节点的左子树不空，则左子树上所有节点的值均小于它的根节点的值；
- 若任意节点的右子树不空，则右子树上所有节点的值均大于或等于它的根节点的值；
- 任意节点的左、右子树也分别为二叉查找树；

#### 基于算法思想——二分搜索

| index | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    |
| ----- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| value | 3    | 5    | 13   | 23   | 39   | 53   | 61   | 72   |

**root(mid) = (low+high)/2** 

![二分搜索树](/Users/whitestorm/Downloads/IMG_60EC1B5846C8-1.jpeg)

#### 结构设计

- 节点

```java
class Node{
    private int value;
    private Node left;
    private Node right;
    public Node(int initValue) {
        this.value = initValue;
    }
    public int getValue(){
        return value;
    }
    public Node getLeft(){
        return this.left;
    }
    public Node getRight(){
        return this.right;
    }
    public void setLeft(Node root){
        this.left = root;
    }
    public void setRight(Node root){
        this.right = right;
    }
}

```

#### 功能设计——add

```java
public void add(Node node,Node head){
    if(node == null){
        return;
    }
    if(node.getValue() < head.getValue()){
        if(head.getLeft() == null){
            head.setLeft(node);
        }
        else {
            add(node,head.getLeft());
        }
    }
    if(node.getValue() > head.getValue()){
        if(head.getRight() == null){
            head.setRight(node);
        }
        else {
            add(node,head.getRight());
        }
    }
}
```

#### 功能设计——search

```java
public void add(Node node,Node head){
    if(node == null){
        return;
    }
    if(node.getValue() < head.getValue()){
        if(head.getLeft() == null){
            head.setLeft(node);
        }
        else {
            add(node,head.getLeft());
        }
    }
    if(node.getValue() > head.getValue()){
        if(head.getRight() == null){
            head.setRight(node);
        }
        else {
            add(node,head.getRight());
        }
    }
}
```

#### 完整源码

```java

 /**
 * @author whiteStorm
 * @date 2020/7/9
 */
public class BinarySortTree {
    public void add(Node node,Node head){
        if(node == null){
            return;
        }
        if(node.getValue() < head.getValue()){
            if(head.getLeft() == null){
                head.setLeft(node);
            }
            else {
                add(node,head.getLeft());
            }
        }
        if(node.getValue() > head.getValue()){
            if(head.getRight() == null){
                head.setRight(node);
            }
            else {
                add(node,head.getRight());
            }
        }
    }
    public Node search(int value,Node head){
        if(head == null){
            return null;
        }
        if(head.getValue() == value){
            return head;
        }
        if(head.getValue() < value){
            if(head.getLeft() != null){
               return search(value,head.getLeft());
            }
            else{
                return null;
            }
        }
        if(head.getValue() > value){
            if(head.getRight() != null){
              return   search(value,head.getRight());
            }
            else {
                return null;
            }
        }
        return null;
    }
}
class Node{
    private int value;
    private Node left;
    private Node right;
    public Node(int initValue) {
        this.value = initValue;
    }
    public int getValue(){
        return value;
    }
    public Node getLeft(){
        return this.left;
    }
    public Node getRight(){
        return this.right;
    }
    public void setLeft(Node root){
        this.left = root;
    }
    public void setRight(Node root){
        this.right = right;
    }
}

```

### 广度优先搜索	

#### 定义：根据节点的深度对树进行遍历

#### 图画演示

![二分搜索树](/Users/whitestorm/Downloads/IMG_60EC1B5846C8-1.jpeg)

![递归](/Users/whitestorm/Downloads/IMG_30EDFED49CEB-1.jpeg)

#### 辅助存储结构

``` java
List<List<Integer>> lists = new ArrayList<>();//层次存储遍历结果
List<TreeNode> nodes = new ArrayList<>(); 		//存储node节点
List<Integer> list = new ArrayList<>();  			//存储每一层遍历结果
```



#### 完整源码

``` java
 public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> lists = new ArrayList<>();
        List<TreeNode> nodes = new ArrayList<>();
        if(root == null){
            return lists;
        }
        nodes.add(root);
        while (!nodes.isEmpty()){
            List<Integer> list = new ArrayList<>();

            int size = nodes.size();

            for(int i = 0;i<size;i++){
                TreeNode node = nodes.remove(0);
                list.add(node.value);
                if(node.left != null)
                {
                    nodes.add(node.left);
                }
                if(node.right != null){
                    nodes.add(node. right);
                }
            }
            lists.add(list);
        }
        return lists;
    }
```


