# Trees

## **Program1**

You are developing an application for a garden management system where each tree

in the garden is represented as a binary tree structure. The system needs to

allow users to plant new trees in a systematic way, ensuring that each tree is

filled level by level.

A gardener wants to:

- Plant trees based on user input.

- Ensure trees grow in a balanced way by filling nodes level by level.

- Inspect the garden layout by performing an in-order traversal, which helps

analyze the natural arrangement of trees.

Your task is to implement a program that:

- Accepts a list of N tree species (as integers).

- Builds a binary tree using level-order insertion.

- Displays the in-order traversal of the tree.

Input Format:

- ------------
- An integer N representing the number of tree plants.
- A space-separated list of N integers representing tree species.

Output Format:

- -------------

A list of integers, in-order traversal of tree.

Sample Input:

- ------------

7

1 2 3 4 5 6 7

Sample Output:

- -------------

4 2 5 1 6 3 7

Explanation:

- -----------

The tree looks like this:

1

/ \

2   3

/ \  / \

4   5 6  7

The in order is : 4 2 5 1 6 3 7

```java
import java.util.*;

class Tree{
    int data;
    Tree left, right;
    Tree(int data){
        this.data=data;
        left=null;
        right=null;
    }

}
public class Solution{

    static void buildTree(Tree root, int ele)
    {
        if(root==null)
        {
            root = new Tree(ele);
            return;
        }
        Queue<Tree> q = new LinkedList<>();
        q.add(root);
        while(!q.isEmpty())
        {
            root=q.remove();
            if(root.left==null)
            {
                root.left= new Tree(ele);
                break;
            }
            else{
                q.add(root.left);
            }
            if(root.right==null)
            {
                root.right= new Tree(ele);
                break;
            }
            else{
                q.add(root.right);
            }
        }

    }
    static void inorder(Tree root)
    {
        if(root==null) return;
        inorder(root.left);
        System.out.print(root.data+" ");
        inorder(root.right);
    }
    public static void main (String[] args) {
        Scanner sc = new Scanner(System.in);
        int n=sc.nextInt();
        int arr[] = new int[n];
        for(int i=0;i<n;i++){
            arr[i]=sc.nextInt();
        }
        Tree root = new Tree(arr[0]);
        for(int i=1;i<n;i++)
            buildTree(root,arr[i]);
        inorder(root);

    }
}
```

## **Program2**

Write a program to construct a binary tree from level-order input, while treating -1

as a placeholder for missing nodes. The program reads input, constructs the tree,

and provides an in-order traversal to verify correctness.

Input Format:

- --------------

Space separated integers, level order data (where -1 indiactes null node).

Output Format:

- ----------------

Print the in-order data of the tree.

Sample Input:

- ---------------

1 2 3 -1 -1 4 5

Sample Output:

- ---------------

2 1 4 3 5

Explanation:

- -------------

1

/ \

2   3

/ \

4   5

Sample Input:

- ---------------

1 2 3 4 5 6 7

Sample Output:

- ---------------

4 2 5 1 6 3 7

Explanation:

- -------------

1

/ \

2   3

/ \  / \

4  5 6  7

```java
import java.util.*;
class Tree{
    int data;
    Tree left,right;
    Tree(int data){
        this.data=data;
        left=null;
        right=null;
    }
}
public class Solution{
    static void buildTree(int[] arr){
        Tree root = new Tree(arr[0]);
        Queue<Tree> q = new LinkedList<>();
        int ind=0;
        int n=arr.length;
        q.add(root);
        while(!q.isEmpty()){
            Tree node = q.poll();
            if(ind+1<n){
                if(arr[ind+1]!=-1)
                {
                    node.left=new Tree(arr[ind+1]);
                    q.add(node.left);
                }
            }
            ind++;
            if(ind+1<n){
                if(arr[ind+1]!=-1)
                {
                    node.right=new Tree(arr[ind+1]);
                    q.add(node.right);
                }
            }
            ind++;
        }

        inorder(root);
    }

    static void inorder(Tree root){
        if(root==null) return;
        inorder(root.left);
        System.out.print(root.data+" ");
        inorder(root.right);

    }
    public static void main(String[] args){
        Scanner sc=new Scanner(System.in);
        String s[]=sc.nextLine().split(" ");
        int n=s.length;
        int arr[] = new int[n];
        for(int i=0;i<n;i++) arr[i]=Integer.parseInt(s[i]+"");

        buildTree(arr);

    }

}
```

## **Program3**

Given the in-order and post-order traversals of a binary tree, construct

the original binary tree. For the given Q number of queries,

each query consists of a lower level and an upper level.

The output should list the nodes in the order they appear in a level-wise.

Input Format:

An integer N representing the number nodes.

A space-separated list of N integers representing the similar to in-order traversal.

A space-separated list of N integers representing the similar to post-order traversal.

An integer Q representing the number of queries.

Q pairs of integers, each representing a query in the form:

Lower level (L)

Upper level (U)

Output Format:

For each query, print the nodes in order within the given depth range

Example

Input:

7

4 2 5 1 6 3 7

4 5 2 6 7 3 1

2

1 2

2 3

Output:

[1, 2, 3]

[2, 3, 4, 5, 6, 7]

Explanation:

1

/ \

2   3

/ \  / \

4   5 6  7

Query 1 (Levels 1 to 2): 1 2 3

Query 2 (Levels 2 to 3): 2 3 4 5 6 7

```java
import java.util.*;

class Tree{
    int data;
    Tree left;
    Tree right;
    Tree(int data){
        this.data=data;
        left=null;
        right=null;
    }
}

class Solution{

    static Tree BuildTree(int in[], int[] po, int start, int end,HashMap<Integer,Integer> map,Stack<Integer> s)
    {

        if(start>end) return null;

        int curr = s.peek();
        s.pop();
        Tree root = new Tree(curr);
        if(start==end) return root;
        int pos = map.get(curr);
        root.right = BuildTree(in,po,pos+1,end,map,s);
        root.left = BuildTree(in,po,start,pos-1,map,s);

        return root;
    }
    static List<List<Integer>> levelOrder(Tree root){
        List<List<Integer>> levels = new ArrayList<>();
        if (root == null) return levels;
        Queue<Tree> q = new LinkedList<>();
        q.offer(root);
        while (!q.isEmpty()) {
            int size = q.size();
            List<Integer> level = new ArrayList<>();
            for (int i = 0; i < size; i++) {
                Tree node = q.poll();
                level.add(node.data);
                if (node.left != null) q.offer(node.left);
                if (node.right != null) q.offer(node.right);
            }
            levels.add(level);
        }
        return levels;
    }
    public static void main (String[] args) {
        Scanner sc = new Scanner(System.in);
        int n=sc.nextInt();
        int in[] = new int[n];
        int po[] = new int[n];
        for(int i=0;i<n;i++) in[i]=sc.nextInt();
        for(int i=0;i<n;i++) po[i]=sc.nextInt();

        HashMap<Integer,Integer> map = new HashMap<>();
        Stack<Integer> s = new Stack<>();
        for(int i=0;i<n;i++)
        {
            map.put(in[i],i);
            s.add(po[i]);
        }

        Tree root = BuildTree(in,po,0,n-1,map,s);

        // inorder(root);

        int q=sc.nextInt();

        List<List<Integer>> ans = new ArrayList<>();
        ans = levelOrder(root);

        List<List<Integer>> finans = new ArrayList<>();

        for(int i=0;i<q;i++){
            int l=sc.nextInt();
            int r=sc.nextInt();

            List<Integer> res = new ArrayList<>();
            for(int j=l;j<=r;j++)
            {
              res.addAll(ans.get(j-1));
            }

            finans.add(res);
        }

        for(int i=0;i<q;i++){
            System.out.println(finans.get(i));
        }

    }

}
```

## **Program4**

Construct the binary tree from the given In-order and Pre-order.

Find Nodes Between Two Levels in Spiral Order.

The spiral order is as follows:

- > Odd levels → Left to Right.
- > Even levels → Right to Left.

## **Input Format:**

An integer N representing the number of nodes.

A space-separated list of N integers representing the in-order traversal.

A space-separated list of N integers representing the pre-order traversal.

Two integers:

Lower Level (L)

Upper Level (U)

Output Format:

Print all nodes within the specified levels, but in spiral order.

Example:

Input:

7

4 2 5 1 6 3 7

1 2 4 5 3 6 7

2 3

Output:

3 2 4 5 6 7

Explanation:

Binary tree structure:

1

/ \

2   3

/ \  / \

4   5 6  7

Levels 2 to 3 in Regular Order:

Level 2 → 2 3

Level 3 → 4 5 6 7

Spiral Order:

Level 2 (Even) → 3 2 (Right to Left)

Level 3 (Odd) → 4 5 6 7 (Left to Right)

```java
import java.util.*;

class Tree{
    int data;
    Tree left;
    Tree right;
    Tree(int data){
        this.data=data;
        left=null;
        right=null;
    }
}

class Solution{

    static Tree BuildTree(int in[], int[] pre, int start, int end,HashMap<Integer,Integer> map,Queue<Integer> q)
    {

        if(start>end) return null;

        int curr = q.poll();
        Tree root = new Tree(curr);
        if(start==end) return root;
        int pos = map.get(curr);
        root.left = BuildTree(in,pre,start,pos-1,map,q);
        root.right = BuildTree(in,pre,pos+1,end,map,q);

        return root;
    }
    static List<List<Integer>> levelOrder(Tree root){
        List<List<Integer>> levels = new ArrayList<>();
        if (root == null) return levels;
        Queue<Tree> q = new LinkedList<>();
        q.offer(root);
        while (!q.isEmpty()) {
            int size = q.size();
            List<Integer> level = new ArrayList<>();
            for (int i = 0; i < size; i++) {
                Tree node = q.poll();
                level.add(node.data);
                if (node.left != null) q.offer(node.left);
                if (node.right != null) q.offer(node.right);
            }
            levels.add(level);
        }
        return levels;
    }

    public static void main (String[] args) {
        Scanner sc = new Scanner(System.in);
        int n=sc.nextInt();
        int in[] = new int[n];
        int pre[] = new int[n];
        for(int i=0;i<n;i++) in[i]=sc.nextInt();
        for(int i=0;i<n;i++) pre[i]=sc.nextInt();

        HashMap<Integer,Integer> map = new HashMap<>();
        Queue<Integer> q = new LinkedList<>();
        for(int i=0;i<n;i++)
        {
            map.put(in[i],i);
            q.add(pre[i]);
        }

        Tree root = BuildTree(in,pre,0,n-1,map,q);

        List<List<Integer>> ans = new ArrayList<>();
        ans = levelOrder(root);

        int l=sc.nextInt();
        int r=sc.nextInt();
        for(int i=l;i<=r;i++)
        {
          if(i%2==0)
          {
            for(int j=ans.get(i-1).size()-1;j>=0;j--)
            {
              System.out.print(ans.get(i-1).get(j)+" ");
            }
          }
          else
          {
            for(int j=0;j<ans.get(i-1).size();j++)
            {
              System.out.print(ans.get(i-1).get(j)+" ");
            }
          }
        }

    }

}

```

## **Program5**

Given the preorder and postorder traversals of a binary tree, construct

the original binary tree and print its level order traversal.

## **Input Format:**

Space separated integers, pre order data

Space separated integers, post order data

## **Output Format:**

Print the level-order data of the tree.

## **Sample Input:**

1 2 4 5 3 6 7

4 5 2 6 7 3 1

## **Sample Output:**

[[1], [2, 3], [4, 5, 6, 7]]

## **Explanation:**

```
    1
   / \\
  2   3
 / \\  / \\
4   5 6  7

```

## **Sample Input:**

1 2 3

2 3 1

## **Sample Output:**

[[1], [2, 3]]

## **Explanation:**

```
1

```

/ \

2  3

```java
import java.util.*;

class Tree{
    int data;
    Tree left;
    Tree right;
    Tree(int data){
        this.data=data;
        this.left=null;
        this.right=null;
    }
}

class Solution{

    static Tree buildTree(Queue<Integer> pre, int[] pos, HashMap<Integer, Integer> posMap, int start, int end) {
        if (pre.isEmpty() || start > end) return null;

        Tree root = new Tree(pre.poll());

        if (start == end) return root;

        int next = posMap.get(pre.peek());

        if (next >= start && next < end) {
            root.left = buildTree(pre, pos, posMap, start, next);
            root.right = buildTree(pre, pos, posMap, next + 1, end - 1);
        }

        return root;
    }

    static List<List<Integer>> levelOrder(Tree root)
    {

        Queue<Tree> q = new LinkedList<>();
        q.add(root);
        List<List<Integer>> ans = new ArrayList<>();
        while(!q.isEmpty())
        {
            int size=q.size();
            List<Integer> temp = new ArrayList<>();
            for(int i=0;i<size;i++){
                Tree node = q.poll();
                if(node.left!=null) q.add(node.left);
                if(node.right!=null) q.add(node.right);
                temp.add(node.data);
            }
            ans.add(temp);
        }
        return ans;
    }

    public static void main (String[] args) {
        Scanner sc = new Scanner(System.in);
        String[] pr = sc.nextLine().split(" ");
        String[] po = sc.nextLine().split(" ");

        int[] pos = new int[po.length];
        Queue<Integer> q = new LinkedList<>();
        HashMap<Integer,Integer> posMap = new HashMap<>();

        for(int i=0;i<pr.length;i++)
        {
            pos[i] = Integer.parseInt(po[i]);
            posMap.put(pos[i],i);
            q.add(Integer.parseInt(pr[i]));
        }
        Tree root = buildTree(q,pos,posMap,0,pos.length-1);

        List<List<Integer>> ans = levelOrder(root);
        System.out.println(ans);

    }
}
```

## **Program6 (Right view)**

Balbir Singh is working with Binary Trees.

The elements of the tree are given in level-order format.

Balbir is observing the tree from the right side, meaning he

can only see the rightmost nodes (one node per level).

You are given the root of a binary tree. Your task is to determine

the nodes visible from the right side and return them in top-to-bottom order.

## **Input Format:**

Space separated integers, elements of the tree.

## **Output Format:**

A list of integers representing the node values visible from the right side

## **Sample Input-1:**

1 2 3 5 -1 -1 5

## **Sample Output-1:**

[1, 3, 5]

## **Sample Input-2:**

3 2 4 3 2

## **Sample Output-2:**

[3, 4, 2]

```java
import java.util.*;

class Tree{
    int data;
    Tree left=null;
    Tree right=null;
    Tree(int data)
    {this.data=data;}
}

class Solution{

    static Tree buildTree(int[] arr)
    {
        Tree root1 = new Tree(arr[0]);
        int ind=0;
        Queue<Tree> q = new LinkedList<>();
        q.add(root1);
        while(ind<arr.length)
        {
            Tree root = q.poll();
           if(ind+1<arr.length)
           {
               if(arr[ind+1]!=-1)
               {
                   root.left = new Tree(arr[ind+1]);
                   q.add(root.left);
               }
           }
           ind++;
           if(ind+1<arr.length)
           {
               if(arr[ind+1]!=-1)
               {
                   root.right=new Tree(arr[ind+1]);
                   q.add(root.right);
               }
           }
           ind++;
        }
        return root1;
    }
    static void rightView(Tree root,int depth, List<Integer> ans)
    {
        if(root==null) return;

        if(depth == ans.size()) ans.add(root.data);
        rightView(root.right,depth+1,ans);
        rightView(root.left,depth+1,ans);
    }
    public static void main (String[] args) {
        Scanner sc = new Scanner(System.in);
        String s[] = sc.nextLine().split(" ");
        int arr[] = new int[s.length];
        for(int i=0;i<s.length;i++) arr[i]=Integer.parseInt(s[i]);

        Tree root = buildTree(arr);

        List<Integer> ans = new ArrayList<>();
        rightView(root,0,ans);
        System.out.println(ans);
    }
}

```

## **Program7 (Boundary Traversal)**

The Indian Army has established multiple military camps at strategic locations

along the Line of Actual Control (LAC) in Galwan. These camps are connected in

a hierarchical structure, with a main base camp acting as the root of the network.

To fortify national security, the Government of India has planned to deploy

a protective S.H.I.E.L.D. that encloses all military camps forming the outer

boundary of the network.

Structure of Military Camps:

- Each military camp is uniquely identified by an integer ID.
- A camp can have at most two direct connections:
- Left connection → Represents a subordinate camp on the left.
- Right connection → Represents a subordinate camp on the right.
- If a military camp does not exist at a specific position, it is

represented by -1

Mission: Deploying the S.H.I.E.L.D.

Your task is to determine the list of military camp IDs forming the outer

boundary of the military network. This boundary must be traversed in

anti-clockwise order, starting from the main base camp (root).

The boundary consists of:

1. The main base camp (root).
2. The left boundary:
    - Starts from the root’s left child and follows the leftmost path downwards.
    - If a camp has a left connection, follow it.
    - If no left connection exists but a right connection does, follow the right connection.
    - The leftmost leaf camp is NOT included in this boundary.
3. The leaf camps (i.e., camps with no further connections), ordered from left to right.
4. The right boundary (in reverse order):
    - Starts from the root’s right child and follows the rightmost path downwards.
    - If a camp has a right connection, follow it.
    - If no right connection exists but a left connection does, follow the left connection.
    - The rightmost leaf camp is NOT included in this boundary.

## **Input Format:**

space separated integers, military-camp IDs.

## **Output Format:**

Print all the military-camp IDs, which are at the edge of S.H.I.E.L.D.

## **Sample Input-1:**

5 2 4 7 9 8 1

## **Sample Output-1:**

[5, 2, 7, 9, 8, 1, 4]

## **Sample Input-2:**

11 2 13 4 25 6 -1 -1 -1 7 18 9 10

## **Sample Output-2:**

[11, 2, 4, 7, 18, 9, 10, 6, 13]

## **Sample Input-3:**

1 2 3 -1 -1 -1 5 -1 6 7

## **Sample Output-3:**

[1, 2, 7, 6, 5, 3]

```java
import java.util.*;

class Node{

    int data;
    Node left;
    Node right;

    Node(int data){
        this.data = data;
    }
}

class Solution{

    static Node buildTree(int [] arr){

        int ind=0;
        Node root = new Node(arr[0]);
        Queue<Node> q = new LinkedList<>();
        q.offer(root);
        ind++;
        while(ind<arr.length){
            Node node = q.poll();
            if(ind < arr.length){
                if(arr[ind] != -1){
                    node.left = new Node(arr[ind]);
                    q.offer(node.left);
                }
            }
            ind++;
            if(ind < arr.length){
                if(arr[ind] != -1){
                    node.right = new Node(arr[ind]);
                    q.offer(node.right);
                }
            }
            ind++;
        }

        return root;
    }

    static void Inorder(Node root){

        if(root == null) return;
        Inorder(root.left);
        System.out.print(root.data+" ");
        Inorder(root.right);
    }

    static void func(Node root , ArrayList<Integer> a){
        if(root == null) return;
        a.add(root.data);

        lb(root.left,a);
        leaves(root.left,a);
        leaves(root.right,a);
        rb(root.right,a);

        return ;
    }

    static void lb(Node root, ArrayList<Integer> a){

        if(root == null) return;
        if(root.left == null && root.right == null) return;

        a.add(root.data);
        if(root.left !=null){
            lb(root.left,a);
        }else{
            lb(root.right,a);
        }
    }

    static void rb(Node root, ArrayList<Integer> a){

        if(root == null) return;
        if(root.left == null && root.right == null) return;

        if(root.right !=null){
            rb(root.right,a);
        }else{
            rb(root.left,a);
        }
        a.add(root.data);
    }

    static void leaves(Node root, ArrayList<Integer> a){

        if(root == null) return;
        if(root.left == null && root.right == null){

            a.add(root.data);
            return;
        }

        leaves(root.left,a);
        leaves(root.right,a);

    }

    public static void main (String[] args) {

        Scanner sc = new Scanner(System.in);
        String[] preo = sc.nextLine().split(" ");
        int n = preo.length;
        int list[] = new int[n];
        for(int i=0;i<n;i++){
            list[i] = Integer.parseInt(preo[i]);
        }

        Node root = buildTree(list);
        // Inorder(root);
        ArrayList<Integer> a = new ArrayList<>();
        func(root,a);
        System.out.println(a);

    }
}

```

## **Program8 (LEFT VIEW OF BT)**

A software development company is designing a smart home automation

system that uses sensor networks to monitor and control different devices

in a house. The sensors are organized in a hierarchical structure, where each

sensor node has a unique ID and can have up to two child nodes (left and right).

The company wants to analyze the left-most sensors in the system to determine

which ones are critical for detecting environmental changes. The hierarchy of

the sensors is provided as a level-order input, where missing sensors are

represented as -1.

Your task is to build the sensor network as a binary tree and then determine

the left-most sensor IDs at each level.

## **Input Format:**

Space separated integers, elements of the tree.

## **Output Format:**

A list of integers representing the left-most sensor IDs at each level

## **Sample Input-1:**

1 2 3 4 -1 -1 5

## **Sample Output-1:**

[1, 2, 4]

## **Sample Input-2:**

3 2 4 1 5

## **Sample Output-2:**

[3, 2, 1]

```java
import java.util.*;

class Tree{
    int data;
    Tree left;
    Tree right;
    Tree(int data)
    {
        this.data=data;
        left=null;
        right=null;
    }
}
class Solution{
    static Tree buildTree(int[] arr)
    {
        Tree root1 = new Tree(arr[0]);
        int ind=0;
        Queue<Tree> q = new LinkedList<>();
        q.add(root1);
        while(ind<arr.length)
        {
            Tree root = q.poll();
           if(ind+1<arr.length)
           {
               if(arr[ind+1]!=-1)
               {
                   root.left = new Tree(arr[ind+1]);
                   q.add(root.left);
               }
           }
           ind++;
           if(ind+1<arr.length)
           {
               if(arr[ind+1]!=-1)
               {
                   root.right=new Tree(arr[ind+1]);
                   q.add(root.right);
               }
           }
           ind++;
        }
        return root1;
    }
    static void leftView(Tree root,int depth, List<Integer> ans)
    {
        if(root==null) return;

        if(depth == ans.size()) ans.add(root.data);
        leftView(root.left,depth+1,ans);
        leftView(root.right,depth+1,ans);
    }
    public static void main (String[] args) {
        Scanner sc = new Scanner(System.in);
        String s[] = sc.nextLine().split(" ");
        int arr[] = new int[s.length];
        for(int i=0;i<s.length;i++) arr[i] = Integer.parseInt(s[i]);

        Tree root = buildTree(arr);
        List<Integer> ans = new ArrayList<>();
        leftView(root,0,ans);
        System.out.println(ans);
    }
}
```

## **Program9**

Distance

Bubloo is working with computer networks, where servers are connected

in a hierarchical structure, represented as a Binary Tree. Each server (node)

is uniquely identified by an integer value.

Bubloo has been assigned an important task: find the shortest communication

path (in terms of network hops) between two specific servers in the network.

## **Network Structure:**

The network of servers follows a binary tree topology.

Each server (node) has a unique identifier (integer).

If a server does not exist at a certain position, it is represented as '-1' (NULL).

Given the root of the network tree, and two specific server IDs (E1 & E2),

determine the minimum number of network hops (edges) required to

communicate between these two servers.

## **Input Format:**

Space separated integers, elements of the tree.

## **Output Format:**

Print an integer value.

## **Sample Input-1:**

1 2 4 3 5 6 7 8 9 10 11 12

4 8

## **Sample Output-1:**

4

## **Explanation:**

The edegs between 4 and 8 are: [4,1], [1,2], [2,3], [3,8]

## **Sample Input-2:**

1 2 4 3 5 6 7 8 9 10 11 12

6 6

## **Sample Output-2:**

0

## **Explanation:**

No edegs between 6 and 6.

```java
import java.util.*;

class Tree {
    int data;
    Tree left = null;
    Tree right = null;

    Tree(int data) {
        this.data = data;
    }
}

class Solution {

    static Tree buildTree(int[] arr) {
        if (arr.length == 0) return null;

        Tree root = new Tree(arr[0]);
        Queue<Tree> q = new LinkedList<>();
        q.add(root);

        int ind = 0;
        while (!q.isEmpty() && ind < arr.length) {
            Tree node = q.poll();

            if (ind + 1 < arr.length && arr[ind + 1] != -1) {
                node.left = new Tree(arr[ind + 1]);
                q.add(node.left);
            }
            ind++;

            if (ind + 1 < arr.length && arr[ind + 1] != -1) {
                node.right = new Tree(arr[ind + 1]);
                q.add(node.right);
            }
            ind++;
        }
        return root;
    }

    static Tree findLCA(Tree root, int src, int dest) {
        if (root == null) return null;
        if (root.data == src || root.data == dest) return root;

        Tree left = findLCA(root.left, src, dest);
        Tree right = findLCA(root.right, src, dest);

        if (left != null && right != null) return root;

        return (left != null) ? left : right;
    }

    static int findLevel(Tree root, int val, int level) {
        if (root == null) return -1;
        if (root.data == val) return level;

        int left = findLevel(root.left, val, level + 1);
        if (left != -1) return left;

        return findLevel(root.right, val, level + 1);
    }

    static int findDist(Tree root, int src, int dest) {
        Tree lca = findLCA(root, src, dest);
        if (lca == null) return -1;

        int d1 = findLevel(lca, src, 0);
        int d2 = findLevel(lca, dest, 0);

        return d1 + d2;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String[] s = sc.nextLine().split(" ");
        int arr[] = new int[s.length];

        for (int i = 0; i < s.length; i++) arr[i] = Integer.parseInt(s[i]);

        int src = sc.nextInt();
        int dest = sc.nextInt();

        Tree root = buildTree(arr);
        int dist = findDist(root, src, dest);

        System.out.println(dist!=-1?dist:-1);
    }
}

// approach 2

import java.util.*;
class TreeNode
{
    int data;
    TreeNode left,right;
    public TreeNode(int v){
        this.data=v;
        this.left=null;
        this.right=null;
    }
}
public class prog1
{
    public static void buildGraph(TreeNode root,HashMap<Integer,List<Integer>> graph,HashMap<Integer,Integer> dist,int i){
        if(root==null){
            return;
        }
        List<Integer> l=graph.getOrDefault(root.data,new ArrayList<>());
        if(root.left!=null){
            l.add(root.left.data);
        }
        if(root.right!=null){
            l.add(root.right.data);
        }
        graph.put(root.data,l);

        dist.put(root.data,i);
        buildGraph(root.left,graph,dist,i+1);
        buildGraph(root.right,graph,dist,i+1);
    }
    public static boolean isInSameTree(HashMap<Integer,List<Integer>> graph,int curNode,int targetNode){
        if(curNode==targetNode){
            return true;
        }
        boolean res=false;
        for(int val:graph.getOrDefault(curNode,new ArrayList<>())){
            res=res||isInSameTree(graph,val,targetNode);
        }
        return res;
    }
    public static int minDistance(TreeNode root,int n1,int n2){
        HashMap<Integer,List<Integer>> graph=new HashMap<>();
        HashMap<Integer,Integer> dist=new HashMap<>();

        buildGraph(root,graph,dist,0);
        // System.out.println("Graph");
        // System.out.println(graph);
        // System.out.println("Distances");
        // System.out.println(dist);
        boolean issame = isInSameTree(graph,n1,n2) || isInSameTree(graph,n2,n1);
        if(issame){
            return Math.abs(dist.get(n1)-dist.get(n2));
        }
        return dist.get(n1)+dist.get(n2);
    }
    public static void main (String[] args) {
        Scanner sc=new Scanner(System.in);

        String[] a=sc.nextLine().split(" ");

        int n=a.length;

        int[] arr=new int[n];

        for(int i=0;i<n;i++){
            arr[i]=Integer.parseInt(a[i]);
        }

        TreeNode root=new TreeNode(arr[0]);
        int idx=0;

        Queue<TreeNode> q=new LinkedList<>();
        q.add(root);

        while(!q.isEmpty()){
            TreeNode p=q.poll();
            if(idx+1<n && arr[idx+1]!=-1){
                p.left=new TreeNode(arr[idx+1]);
                q.add(p.left);
            }
            idx++;

            if(idx+1<n && arr[idx+1]!=-1){
                p.right=new TreeNode(arr[idx+1]);
                q.add(p.right);
            }
            idx++;
        }
        int n1=sc.nextInt();
        int n2=sc.nextInt();
        System.out.println(minDistance(root,n1,n2));
    }

}
```

## **Program10**

Symmetric

Mr. Rakesh is interested in working with Data Structures.

He has constructed a Binary Tree (BT) and asked his friend

Anil to check whether the BT is a self-mirror tree or not.

Can you help Rakesh determine whether the given BT is a self-mirror tree?

Return true if it is a self-mirror tree; otherwise, return false.

## **Note:**

In the tree, '-1' indicates an empty (null) node.

## **Input Format:**

A single line of space separated integers, values at the treenode

## **Output Format:**

Print a boolean value.

## **Sample Input-1:**

2 1 1 2 3 3 2

## **Sample Output-1:**

true

## **Sample Input-2:**

2 1 1 -1 3 -1 3

## **Sample Output-2:**

false

```java
import java.util.*;

class Tree {
    int data;
    Tree left = null;
    Tree right = null;

    Tree(int data) {
        this.data = data;
    }
}

class Solution {

    static Tree buildTree(int[] arr) {
        if (arr.length == 0) return null;

        Tree root = new Tree(arr[0]);
        Queue<Tree> q = new LinkedList<>();
        q.add(root);

        int ind = 0;
        while (!q.isEmpty() && ind < arr.length) {
            Tree node = q.poll();

            if (ind + 1 < arr.length && arr[ind + 1] != -1) {
                node.left = new Tree(arr[ind + 1]);
                q.add(node.left);
            }
            ind++;

            if (ind + 1 < arr.length && arr[ind + 1] != -1) {
                node.right = new Tree(arr[ind + 1]);
                q.add(node.right);
            }
            ind++;
        }
        return root;
    }

    static boolean isSymmetric(Tree root1,Tree root2)
    {
        if(root1==null && root2==null) return true;
        if(root1==null || root2==null || root1.data!=root2.data) return false;

        return isSymmetric(root1.left,root2.right) && isSymmetric(root1.right,root2.left);

        // return false;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String[] s = sc.nextLine().split(" ");
        int arr[] = new int[s.length];

        for (int i = 0; i < s.length; i++) arr[i] = Integer.parseInt(s[i]);

        Tree root = buildTree(arr);
        System.out.println(isSymmetric(root.left,root.right));
    }
}

```

## **Program11**

Balbir Singh is working with networked systems, where servers are connected

in a hierarchical structure, represented as a Binary Tree. Each server (node) has

a certain processing load (integer value).

Balbir has been given a critical task: split the network into two balanced

sub-networks by removing only one connection (edge). The total processing

load in both resulting sub-networks must be equal after the split.

Network Structure:

- The network of servers follows a binary tree structure.
- Each server is represented by an integer value, indicating its processing load.
- If a server does not exist at a particular position, it is represented as '-1' (NULL).

Help Balbir Singh determine if it is possible to split the network into two equal

processing load sub-networks by removing exactly one connection.

## **Input Format:**

Space separated integers, elements of the tree.

## **Output Format:**

Print a boolean value.

## **Sample Input-1:**

1 2 3 5 -1 -1 5

## **Sample Output-1:**

true

## **Sample Input-2:**

3 2 4 3 2 -1 7

## **Sample Output-2:**

false

```java
import java.util.*;

class Tree{
    int data;
    Tree left=null;
    Tree right=null;
    Tree(int data) {this.data=data;}
}

class Solution{
    static Tree buildTree(int[] arr) {
        if (arr.length == 0) return null;

        Tree root = new Tree(arr[0]);
        Queue<Tree> q = new LinkedList<>();
        q.add(root);

        int ind = 1;
        while (!q.isEmpty() && ind < arr.length) {
            Tree node = q.poll();

            if (ind < arr.length && arr[ind] != -1) {
                node.left = new Tree(arr[ind]);
                q.add(node.left);
            }
            ind++;

            if (ind < arr.length && arr[ind] != -1) {
                node.right = new Tree(arr[ind]);
                q.add(node.right);
            }
            ind++;
        }
        return root;
    }

    static int totalSum;

    static boolean check(Tree root) {
        totalSum = sum(root);
        if (totalSum % 2 != 0) return false;
        return findPartition(root, new int[1]);
    }

    static int sum(Tree root) {
        if (root == null) return 0;
        return root.data + sum(root.left) + sum(root.right);
    }

    static boolean findPartition(Tree root, int[] subSum) {
        if (root == null) return false;

        int leftSum = sum(root.left);
        int rightSum = sum(root.right);

        if (leftSum == totalSum - leftSum || rightSum == totalSum - rightSum) return true;

        return findPartition(root.left, subSum) || findPartition(root.right, subSum);
    }

    public static void main (String[] args) {
        Scanner sc = new Scanner(System.in);
        String[] s = sc.nextLine().split(" ");
        int arr[] = new int[s.length];

        for (int i = 0; i < s.length; i++) arr[i] = Integer.parseInt(s[i]);

        Tree root = buildTree(arr);
        System.out.println(check(root));
    }
}

```

## **Program12**

Balbir Singh is working with Binary Trees.

The elements of the tree is given in the level order format.

Balbir has a task to split the tree into two parts by removing only one edge

in the tree, such that the product of sums of both the splitted-trees should be maximum.

You will be given the root of the binary tree.

Your task is to help the Balbir Singh to split the binary tree as specified.

print the product value, as the product may be large, print the (product % 1000000007)

NOTE:

Please do consider the node with data as '-1' as null in the given trees.

## **Input Format:**

Space separated integers, elements of the tree.

## **Output Format:**

Print an integer value.

## **Sample Input-1:**

1 2 4 3 5 6

## **Sample Output-1:**

110

## **Explanation:**

if you split the tree by removing edge between 1 and 4,

then the sums of two trees are 11 and 10. So, the max product is 110.

## **Sample Input-2:**

3 2 4 3 2 -1 6

## **Sample Output-2:**

100

```java

import java.util.*;

class Tree{
    int data;
    Tree left=null;
    Tree right=null;
    Tree(int data) {this.data=data;}
}

class Solution{
    static Tree buildTree(int[] arr) {
        if (arr.length == 0) return null;

        Tree root = new Tree(arr[0]);
        Queue<Tree> q = new LinkedList<>();
        q.add(root);

        int ind = 1;
        while (!q.isEmpty() && ind < arr.length) {
            Tree node = q.poll();

            if (ind < arr.length && arr[ind] != -1) {
                node.left = new Tree(arr[ind]);
                q.add(node.left);
            }
            ind++;

            if (ind < arr.length && arr[ind] != -1) {
                node.right = new Tree(arr[ind]);
                q.add(node.right);
            }
            ind++;
        }
        return root;
    }

    static int totalSum;

    static int check(Tree root, int[] prod) {
        totalSum = sum(root);
        prod[0]=0;
        findPartition(root,prod);
        return prod[0];
    }

    static int sum(Tree root) {
        if (root == null) return 0;
        return root.data + sum(root.left) + sum(root.right);
    }

    static void findPartition(Tree root,int prod[]) {
        if (root == null) return ;

        int leftSum = sum(root.left);
        int rightSum = sum(root.right);

        prod[0] = Math.max(prod[0],(leftSum*(totalSum-leftSum)));
        prod[0] = Math.max(prod[0],(rightSum*(totalSum-rightSum)));
         findPartition(root.left,prod); findPartition(root.right,prod);
    }

    public static void main (String[] args) {
        Scanner sc = new Scanner(System.in);
        String[] s = sc.nextLine().split(" ");
        int arr[] = new int[s.length];

        for (int i = 0; i < s.length; i++) arr[i] = Integer.parseInt(s[i]);

        Tree root = buildTree(arr);
        int prod[] = new int[1];
        check(root,prod);
        System.out.println(prod[0] % 1000000007);
    }
}

```

## **Program13**

Imagine you are a librarian organizing books on vertical shelves in a grand

library. The books are currently scattered across a tree-like structure, where

each book (node) has a position determined by its shelf number (column) and row

number (level).

Your task is to arrange the books on shelves so that:

1. Books are placed column by column from left to right.
2. Within the same column, books are arranged from top to bottom (i.e., by row).
3. If multiple books belong to the same shelf and row, they should be arrangedfrom left to right, just as they appear in the original scattered arrangement.

## **Sample Input:**

3 9 20 -1 -1 15 7

## **Sample Output:**

[[9],[3,15],[20],[7]]

## **Explanation:**

```
     3
   /   \\
  9     20
      /    \\
     15     7

```

Shelf 1: [9]

Shelf 2: [3, 15]

Shelf 3: [20]

Shelf 4: [7]

## **Sample Input-2:**

3 9 8 4 0 1 7

## **Sample Output-2:**

[[4],[9],[3,0,1],[8],[7]]

## **Explanation:**

```
      3
   /     \\
  9       8
/   \\   /   \\

```

4     0 1     7

Shelf 1: [4]

Shelf 2: [9]

Shelf 3: [3, 0, 1]

Shelf 4: [8]

Shelf 5: [7]

```java
import java.util.*;

class Tree{
    int data;
    Tree left=null;
    Tree right=null;
    Tree(int data) {this.data=data;}
}

class Pair{
    Tree node;
    int x;
    int y;
    Pair(Tree node,int x, int y)
    {
        this.node=node;
        this.x=x;
        this.y=y;
    }
}

class Solution{
    static Tree buildTree(int[] arr) {
        if (arr.length == 0) return null;

        Tree root = new Tree(arr[0]);
        Queue<Tree> q = new LinkedList<>();
        q.add(root);

        int ind = 1;
        while (!q.isEmpty() && ind < arr.length) {
            Tree node = q.poll();

            if (ind < arr.length && arr[ind] != -1) {
                node.left = new Tree(arr[ind]);
                q.add(node.left);
            }
            ind++;

            if (ind < arr.length && arr[ind] != -1) {
                node.right = new Tree(arr[ind]);
                q.add(node.right);
            }
            ind++;
        }
        return root;
    }

    static void verticalOrder(Tree root)
    {
        Map<Integer,ArrayList<Integer>> nodes = new TreeMap<>();

        Queue<Pair> q = new LinkedList<>();

        q.add(new Pair(root,0,0));

        while(!q.isEmpty())
        {
            Pair p  =q.poll();

            Tree temp=p.node;
            int x=p.x;
            int y=p.y;

            nodes.computeIfAbsent(x,k-> new ArrayList<>()).add(temp.data);

            if(temp.left!=null) q.add(new Pair(temp.left,x-1,y+1));
            if(temp.right!=null) q.add(new Pair(temp.right,x+1,y+1));
        }

        List<List<Integer>> ans = new ArrayList<>();

        for(ArrayList<Integer> entry: nodes.values()){

            ans.add(entry);
        }

        System.out.println(ans);
    }

    public static void main (String[] args) {
        Scanner sc = new Scanner(System.in);
        String[] s = sc.nextLine().split(" ");
        int arr[] = new int[s.length];

        for (int i = 0; i < s.length; i++) arr[i] = Integer.parseInt(s[i]);

        Tree root = buildTree(arr);

        verticalOrder(root);

    }
}

```

## **Program14**

You are a gardener designing a beautiful floral pathway in a vast botanical

garden. The garden is currently overgrown with plants, trees, and bushes

arranged in a complex branching structure, much like a binary tree. Your task

is to carefully prune and rearrange the plants to form a single-file walking

path that visitors can follow effortlessly.

To accomplish this, you must flatten the garden’s layout into a linear sequence

while following these rules:

1. The garden path should maintain the same PlantNode structure,

where the right branch connects to the next plant in the sequence,

and the left branch is always trimmed (set to null).

2. The plants in the final garden path should follow the same arrangement

as a pre-order traversal of the original garden layout.

## **Input Format:**

Space separated integers, elements of the tree.

## **Output Format:**

Print the list.

## **Sample Input:**

1 2 5 3 4 -1 6

## **Sample Output:**

1 2 3 4 5 6

## **Explanation:**

input structure:

1

/ \

2   5

/ \    \

3   4    6

output structure:

1

\

2

\

3

\

4

\

5

\

6

```java

import java.util.*;

class Tree{
    int data;
    Tree left=null;
    Tree right=null;
    Tree(int data) {this.data=data;}
}

class Solution{
    static Tree buildTree(int[] arr) {
        if (arr.length == 0) return null;

        Tree root = new Tree(arr[0]);
        Queue<Tree> q = new LinkedList<>();
        q.add(root);

        int ind = 1;
        while (!q.isEmpty() && ind < arr.length) {
            Tree node = q.poll();

            if (ind < arr.length && arr[ind] != -1) {
                node.left = new Tree(arr[ind]);
                q.add(node.left);
            }
            ind++;

            if (ind < arr.length && arr[ind] != -1) {
                node.right = new Tree(arr[ind]);
                q.add(node.right);
            }
            ind++;
        }
        return root;
    }

    static void buildList(Tree root)
    {
        if(root==null) return;

        Tree left=root.left;
        Tree right=root.right;

        Tree temp=left;
        while(temp!=null && temp.right!=null) temp=temp.right;

        if(temp!=null)
            temp.right=right;

        root.right=(left!=null)?left:right;
        root.left=null;

        buildList(root.right);

    }

    static void level(Tree root){
        Queue<Tree> q = new LinkedList<>();
        q.add(root);
        while(!q.isEmpty())
        {
            int s=q.size();
            for(int i=0;i<s;i++)
            {
                Tree n=q.poll();
                System.out.print(n.data+" ");
                if(n.left!=null) q.add(n.left);
                if(n.right!=null) q.add(n.right);
            }
        }
    }
    static void inorder(Tree root){
        if(root==null) return;
        inorder(root.left);
        System.out.print(root.data+" ");
        inorder(root.right);
    }

    public static void main (String[] args) {
        Scanner sc = new Scanner(System.in);
        String[] s = sc.nextLine().split(" ");
        int arr[] = new int[s.length];

        for (int i = 0; i < s.length; i++) arr[i] = Integer.parseInt(s[i]);

        Tree root = buildTree(arr);

        buildList(root);

        level(root);

    }
}
```