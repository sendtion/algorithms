课程回顾：[http://www.nowcoder.com/live/11/6/1](http://www.nowcoder.com/live/11/6/1)
课件下载：[https://pan.baidu.com/s/1jIbeHeA](https://pan.baidu.com/s/1jIbeHeA)


## 题目一：环形单链表的约瑟夫问题
【题目】
据说著名犹太历史学家Josephus 有过以下故事：在罗马人占领乔塔帕特后，39 个犹太人
与Josephus 及他的朋友躲到一个洞中，39 个犹太人决定宁愿死也不要被敌人抓到，于是
决定了一个自杀方式，41 个人排成一个圆圈，由第1 个人开始报数，报数到3 的人就自
杀，然后再由下一个人重新报1，报数到3 的人再自杀，这样依次下去，直到剩下最后一
个人时，那个人可以自由选择自己的命运。这就是著名的约瑟夫问题。现在请用单向环形链
表描述该结构并呈现整个自杀过程。

输入：一个环形单向链表的头节点head 和报数的值m。  
返回：最后生存下来的节点，且这个节点自己组成环形单向链表，其他节点都删掉。

【要求】
如果链表节点数为N，请实现时间复杂度为O(N)的解法。

    自然想法：O(N* M)
    时间复杂度为O(N)：
        需用数学归纳法，
    1. 先来看A（报数）与B（环形链表元素的编号）的关系         2. 再来看 (没删元素之前的)旧编号 与(删除元素之后的新的链表的)新编号之间的关系：
        A（报数）       B（编号）                               旧编号         新编号
        1               1                                       1               1   
        ·              ·                                      2               2
        ·              ·                                      3               3
        ·              ·                                      4               4
        i-1             i-1                                    ·              ·
        i               i                                      ·              ·
        i+1             1                                      ·              ·
        ·              ·                                     s-2             i-2
        ·              ·                                     s-1             i-1
        ·              ·                                     s               ×（假设要求每次干掉的是第s号元素）
        2i-1            i-1                                   s+1             1
        2i              i                                     s+2             2
        2i+1            i+1                                   ·              ·
        ·              ·                                    ·              ·
        ·              ·                                    ·              ·  
        ·              ·                                    i               i-s
        B = （A-1）% i + 1                                   old = （new + s -1）%i + 1
        即：s = (m -1)%i +1
        old =（new + m -1）%i + 1   
         
    
代码：[https://github.com/nibnait/algorithms/blob/master/src/nowcoder/b_2nd_Season/bf160824/src/Josephus.java](https://github.com/nibnait/algorithms/blob/master/src/nowcoder/b_2nd_Season/bf160824/src/Josephus.java)
        
## 题目二： 判断一个链表是否为回文结构
【题目】
给定一个链表的头节点head，请判断该链表是否为回文结构。
例如：

    1->2->1，返回true。
    1->2->2->1，返回true。
    15->6->15，返回true。
    1->2->3，返回false。
【要求】
如果链表长度为N，时间复杂度达到O(N)，额外空间复杂度达到O(1)

    额外空间复杂度达到O(1)，就不能用栈了。。
    判断是否回文：
![nowcoderbd16081701](https://raw.githubusercontent.com/nibnait/algorithms/master/src/nowcoder/common/imgs/nowcoderbd16081701.png)
        
        
代码：[https://github.com/nibnait/algorithms/blob/master/src/nowcoder/b_2nd_Season/bf160824/src/IsPalindromeList.java](https://github.com/nibnait/algorithms/blob/master/src/nowcoder/b_2nd_Season/bf160824/src/IsPalindromeList.java)


## 题目三： 复制含有随机指针节点的链表
【题目】
一种特殊的链表节点类描述如下：

    public class Node {
        public int value;
        public Node next;
        public Node rand;
        public Node(int data) {
            this.value = data;
        }
    }
Node 类中的value 是节点值，next 指针和正常单链表中next 指针的意义一样，都指向下一个节点，rand 指针是Node
类中新增的指针，这个指针可能指向链表中的任意一个节点，也可能指向null。

给定一个由Node 节点类型组成的无环单链表的头节点head，请实现一个函数完成这个链表中所有结构的复制，并返
回复制的新链表的头节点。例如：链表1->2->3->null，假设1 的rand 指针指向3，2 的rand 指针指向null，3
的rand 指针指向1。复制后的链表应该也是这种结构，比如，1->2->3->null，1 的rand 指针指向3，2 的rand
指针指向null，3 的rand 指针指向1，最后返回1。

【要求】
时间复杂度为O(N)，额外空间复杂度O(1)

    解法一：
        用一个HashMap维持原来正常链表之间各个节点之间的关系
        然后，再遍历一下原链表的rand指针，构造一个rand链表即可
    解法二：
        1 ->2  -> 3
        1 ->1' -> 2 -> 2' -> 3 -> 3'    （这样就是 直接把两个节点的对应关系变成了此节点的next）
        然后遍历rand指针，将1'、2'、3'变成rand指针指向的结点。

代码：[https://github.com/nibnait/algorithms/blob/master/src/nowcoder/b_2nd_Season/bf160824/src/CopyListWithRandom.java](https://github.com/nibnait/algorithms/blob/master/src/nowcoder/b_2nd_Season/bf160824/src/CopyListWithRandom.java)

## 题目四： 一种怪异的节点删除方式
【题目】  
链表节点值类型为int 型，给定一个链表中的节点node，但不给定整个链表的头节点。如何在链表
中删除node？请实现这个函数，并分析这么会出现哪些问题。

【要求】  
时间复杂度为O(1)。

    抖机灵：（借尸还魂）将此结点变成下一个节点，然后删除此结点的下一个节点。
        缺点：
             - 当此节点为尾结点时，无法将此节点变为null（【null为系统中的特定的那块区域！！并无法复制】 并不是因为尾结点下面没有结点了。）
             - 实际开发中，并不能完全复制。.

    所以正常情况下 链表要删除一个节点，必须提供head ！！
    
    


## 题目五： 两个单链表相交的一系列问题
【题目】
在本题中，单链表可能有环，也可能无环。给定两个单链表的头节点head1 和head2，这两个链表可能相交，也可能
不相交。请实现一个函数，如果两个链表相交，请返回相交的第一个节点；如果不相交，返回null 即可。

【要求】
如果链表1 的长度为N，链表2 的长度为M，时间复杂度请达到O(N+M)，额外空间复杂度请达到O(1)。

    先求第一个入环结点：
    快慢指针：F：一次走两步、S：一次走一步
         - 如果有环，则F与S一定会在环中相遇。
            相遇时，再来一个指针A：一次走一步，（S：也一次走一步）
            则A与S 一定会在入环的第一个节点相遇【一定】，可返回入环的第一个节点。
         - 如果无环，
            return null;
                
1. 两个链表：一个有环，一个无环
    则两个链表不可能相交
    return null;
    
2. 两个链表：都无环
     - 不相交 （"||"型）
     - 相交   （"Y " 型）（不可能是"X "型的，因为一个结点只能有一个next元素）
     
    法一：  
        HashMap 保存第一个链表结点之间的关系  
        然后比较第二个链表，
        
    法二：  
        先统计两条链表的长度  
        然后让长链表先把多出来的步数走掉  
        然后两条链表一起走，相遇则“Y”，否则为“||”  

3. 两个链表：都有环
     - 先相交，再共同入环（两个链表的第一个入环结点相等）
     - 共享环，（在环外没遇上）：让环1的入环结点，往下走，如果遇到了环2的入环结点，√
     - 不相交： 两环的入环的第一个节点没遇上 

![nowcoderbd16081702](https://raw.githubusercontent.com/nibnait/algorithms/master/src/nowcoder/common/imgs/nowcoderbd16081702.png)        

    
代码：[https://github.com/nibnait/algorithms/blob/master/src/nowcoder/b_2nd_Season/bf160824/src/FindFirstIntersectNode.java](https://github.com/nibnait/algorithms/blob/master/src/nowcoder/b_2nd_Season/bf160824/src/FindFirstIntersectNode.java)