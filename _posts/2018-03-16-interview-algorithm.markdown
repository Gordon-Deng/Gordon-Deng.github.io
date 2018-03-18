---
layout:     post
title:      "Java 软件工程技术 面试 个人指南 (三) - 常见算法篇"
subtitle:   "\"一切都是为了做个不后悔的自己\""
date:       2018-03-16 12:00:00
author:     "Gordon"
header-img: "img/in-post/2018-03-16-interview-algorithm/interview-algorithm-bg-2.jpg"
catalog: true
tags:
    - Java
    - Interview
    - Algorithm
---
## 数组

## 链表
![](/img/in-post/2018-03-16-interview-algorithm/list-1.gif)

1. 判断单链表中是否有环找到环的入口节点
  * 使用追赶的方法，设定两个指针slow、fast，从头指针开始，每次分别前进1步、2步。如存在环，则两者相遇；如不存在环，fast遇到NULL退出
  
2. 如何知道环的长度
  * 记录下问题1的碰撞点p，slow、fast从该点开始，再次碰撞所走过的操作数就是环的长度s
  
3. 如何找出环的连接点在哪里？
  * **碰撞点p到连接点的距离=头指针到连接点的距离，因此，分别从碰撞点、头指针开始走，相遇的那个点就是连接点。**
  * 假设slow行进了x并在A点进入环路时，fast在环中已经行进了n圈来到B点(n>=0)，其行进距离为2x，则可得到如下等式：2x = x +ns+s-y，做一下运算，即x=(n+1)s-y 
  * 若此时再设置一个指向头节点的指针p，而slow在M处，当p行进了x来到A点时，M行进了x=(n+1)s-y，恰好也来到A处，此时，2个指针相遇了。走的步数即为x长度可知

4. 带环链表的长度是多少？
  * 问题3中已经求出连接点距离头指针的长度，加上问题2中求出的环的长度，二者之和就是带环单链表的长度


## 排序

* 快排过程，复杂度，适用条件

复杂度：期望O(nlgn) 最坏O(n^2)   
适用条件：待排列基本无序

```
public class Quick {
    public void sort(int[] array){
        List<Integer> list = new ArrayList<Integer>();
        for (int i = 0; i < array.length; i++) {
            list.add(array[i]);
        }
        //Collections.shuffle()使数组乱序
        Collections.shuffle(list);

        Iterator<Integer> ite = list.iterator();
        int i = 0;
        while (ite.hasNext()){
            array[i++] = ite.next();
        }

        sort(array, 0, array.length-1);
    }

    private static void sort(int[] a, int low, int high) {
        if (low >= high){
            return;
        }

        int j = partition(a, low, high);
        sort(a, low, j-1);
        sort(a, j+1, high);
    }

    private static int partition(int[] array, int low, int high) {
        int last = array[high];
        int i = low - 1;

        for (int j = low; j < high; j++) {
            if (array[j] <= last){
                i++;
                //用异或做交换运算的两个值不能相同
                if (i != j){
                    //（a ^ b） ^ b=a ^ (b ^ b)=a ^0=a
                    array[i] = array[i]^array[j];
                    array[j] = array[i]^array[j];
                    array[i] = array[i]^array[j];
                }
            }
        }

        if ((i+1) != high){
            array[i+1] = array[i+1]^array[high];
            array[high] = array[i+1]^array[high];
            array[i+1] = array[i+1]^array[high];
        }

        return i+1;
    }
}
```


* 二叉平衡树，增删节点
* 完全二叉树
 
```
class Node {   
    public Node leftchild;
    public Node rightchild;
    public int data;

    public Node(int data) {
        this.data = data;
    }

}

public class TestBinTree {
    
    /**
     * 将一个arry数组构建成一个完全二叉树
     * @param arr 需要构建的数组
     * @return 二叉树的根节点
     */
    public Node initBinTree(int[] arr) {
        if(arr.length == 1) {
            return new Node(arr[0]);
        }
        List<Node> nodeList = new ArrayList<>();
        
        for(int i = 0; i < arr.length; i++) {
            nodeList.add(new Node(arr[i]));
        }
        int temp = 0;
        while(temp <= (arr.length - 2) / 2) { 
        //注意这里，数组的下标是从零开始的
            if(2 * temp + 1 < arr.length) {
                nodeList.get(temp).leftchild = nodeList.get(2 * temp + 1);
            }
            if(2 * temp + 2 < arr.length) {
                nodeList.get(temp).rightchild = nodeList.get(2 * temp + 2);
            }
            temp++;
        }
        return nodeList.get(0);
       }
 
    /**
     * 层序遍历二叉树，，并分层打印
     * @param root 二叉树根节点
     *
     */
     public void trivalBinTree(Node root) {
        Queue<Node> nodeQueue = new ArrayDeque<>(); 
        nodeQueue.add(root);
        Node temp = null;
        int currentLevel = 1;    
        //记录当前层需要打印的节点的数量
        int nextLevel = 0;
        //记录下一层需要打印的节点的数量
        while ((temp = nodeQueue.poll()) != null) {
            if (temp.leftchild != null) {
                nodeQueue.add(temp.leftchild);
                nextLevel++;
                
            }
            if (temp.rightchild != null) {
                nodeQueue.add(temp.rightchild);
                nextLevel++;
            }
            System.out.print(temp.data + " ");
            currentLevel--;
            if(currentLevel == 0) {
                System.out.println();
                currentLevel = nextLevel;
                nextLevel = 0;
            }
        }
    }
    

      /**
       * 先序遍历
       * @param root 二叉树根节点
       */
        public void preTrival(Node root) {
            if(root == null) {
                return;
            }
            System.out.print(root.data + " ");
            preTrival(root.leftchild);
            preTrival(root.rightchild);
        }
        /**
         * 中序遍历
         * @param root 二叉树根节点
         */
        public void midTrival(Node root) {
            if(root == null) {
                return;
            }
            midTrival(root.leftchild);
            System.out.print(root.data + " ");
            midTrival(root.rightchild);
        }
        /**
         * 后序遍历
         * @param root 二叉树根节点
         */
        public void afterTrival(Node root) {
            if(root == null) {
                return;
                
            }
            afterTrival(root.leftchild);
            afterTrival(root.rightchild);
            System.out.print(root.data + " ");
        }
        
        
        public static void main(String[] args) {
            TestBinTree btree = new TestBinTree();
            int[] arr = new int[] {1,2,3,4,5,6,7};
            Node root = btree.initBinTree(arr);
            System.out.println("层序遍历(分层打印)：");
            btree.trivalBinTree(root);
            System.out.println("\n先序遍历：");
            btree.preTrival(root);
            System.out.println("\n中序遍历：");
            btree.midTrival(root);
            System.out.println("\n后序遍历：");
            btree.afterTrival(root);
            
        }
       
     } 
```
* 二分查找
* 10000个数找重复
   * hashset
   * 10001和 减去 10000和
* 一堆数中找和为K的两个数
   * 可以用hash表来存储数组中的元素，这样我们取得一个数后，去判断sum - val 在不在数组中，如果在数组中，则找到了一对二元组，它们的和为sum，该算法的缺点就是需要用到一个hash表，增加了空间复杂度。
   * 同样是基于查找，我们可以先将数组排序，然后依次取一个数后，在数组中用二分查找，查找sum -val是否存在，如果存在，则找到了一对二元组，它们的和为sum，该方法与上面的方法相比，虽然不用实现一个hash表，也没不需要过多的空间，但是时间多了很多。排序需要O(nLogn)，二分查找需要(Logn)，查找n次，所以时间复杂度为O(nLogn)。
   * 该方法基于第2种思路，但是进行了优化，在时间复杂度和空间复杂度是一种折中，但是算法的简单直观、易于理解。首先将数组排序，然后用两个指向数组的指针，一个从前往后扫描，一个从后往前扫描，记为first和last，如果 fist + last < sum 则将fist向前移动，如果fist + last > sum，则last向后移动。








## 字符串
## 栈
## 树
## 分治
## 回溯
## 哈希
## 复杂度
## 动态规划
## 贪心算法