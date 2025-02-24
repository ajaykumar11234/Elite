# Sliding Window

# program 1

You are given an integer array nums and two integers l and r. Your task is to
find the minimum positive energy produced by a sequence of operations.
Each operation corresponds to selecting a contiguous subarray of nums
whose length is between l and r (inclusive).

The energy of a sequence is defined as the product of all the numbers in
the subarray. You need to find the sequence with the smallest positive energy.

If no such sequence exists, return -1.

## Input Format:

Line-1: Three space separated integers, N, L and R.
Line-2: N space separated integers, array[].

## Output Format:

An integer result, smallest positive energy.

## Sample Input-1:

4 2 3
2 -1 3 4

## Sample Output-1:

12

## Explanation:

The possible sequences of operations with lengths between l = 2 and r = 3 are:

[2, -1] (not valid, energy = -2)
[3, 4] (energy = 12)
[2, -1, 3] (not valid, energy = -6)
The sequence [3, 4] produces the smallest positive energy of 12. Hence,
the output is 12.

## Sample Input-2:

3 2 3
-1 -3 2

## Sample Output-1:

- 1

Explanation:
No valid sequence produces a positive energy. Thus, the output is -1.

# Constraints:

1 ≤ nums.length ≤ 100
1 ≤ l ≤ r ≤ nums.length
−1000 ≤ nums[i] ≤ 1000

```java
import java.util.*;

public class MinPositiveEnergy {
    public static int minPositiveEnergy(int[] nums, int L, int R) {
        int n = nums.length;
        int minEnergy = Integer.MAX_VALUE;
        
        // Iterate over all possible start indices
        for (int start = 0; start < n; start++) {
            int product = 1; // Reset product for each new starting index
            
            // Iterate over valid subarrays of length between L and R
            for (int end = start; end < Math.min(n, start + R); end++) {
                product *= nums[end];  // Compute product
                
                // Only consider subarrays of at least length L
                if (end - start + 1 >= L) {
                    if (product > 0) {
                        minEnergy = Math.min(minEnergy, product);
                    }
                }
            }
        }
        
        return (minEnergy == Integer.MAX_VALUE) ? -1 : minEnergy;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        // Read input
        int N = sc.nextInt();
        int L = sc.nextInt();
        int R = sc.nextInt();
        int[] nums = new int[N];
        
        for (int i = 0; i < N; i++) {
            nums[i] = sc.nextInt();
        }
        
        // Compute and print the result
        System.out.println(minPositiveEnergy(nums, L, R));
        
        sc.close();
    }
}

```

# 2.program..

The Kingdom of CodeLand has a long bridge made of square tiles,

where each tile is painted either red ('R') or blue ('B').

A critical mission has been assigned to you: ensure that a section of the

bridge is sturdy enough to support heavy traffic. Blue tiles are reinforced,

while red tiles are weak and need to be reinforced by painting them blue.

You are given a 0-indexed string bridge of length n, where bridge[i] represents the color of the i-th tile. Each character in bridge is either 'R' (red) or 'B' (blue).

Your goal is to ensure that there is at least one segment of k consecutive blue tiles on the bridge to support heavy traffic. You can repaint a red tile ('R') to a blue tile ('B') in one operation.

Write a program to determine the minimum number of repaint operations needed to create a segment of k consecutive blue tiles.

Input Format:

- --------------

Space separated string and integer, S and K

Output Format:

- ----------------

An integer value.

Sample Input-1:

- -----------------

RRBRBBRRBR 4

Sample Output-1:

- -------------------

1

Explanation:

- ------------

One way to achieve 4 consecutive blue tiles is to repaint the 4th tile to get bridge = "RRBBBBRRBR".

This requires 1 operations.

Sample Input-2:

- -----------------

BRBRRBB 3

Sample Output-2:

- -------------------

1

Explanation:

- -------------

One way to achieve 3 consecutive blue tiles is to repaint the 2nd tile to get bridge = "BBBRRBB".

This requires only 1 operation.

Sample Input-3:

- -----------------

BBBRRBRBRR 5

Sample Output-3:

- -------------------

2

Explanation:

- -------------

One way to achieve 5 consecutive blue tiles is to repaint the 4th and 9th tiles to get bridge = "BBBBBBBRRR".

This requires 2 operations.

```java
import java.util.*;
class Solution{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        String s =sc.next();
        int k=sc.nextInt();
        int ans=Integer.MIN_VALUE;
        int len=0;
        int count=0;
        for(int i=0;i<k;i++)
        {
            count+=s.charAt(i)=='B'?1:0;
        }
        ans=Math.max(count,ans);
        for(int i=k;i<s.length();i++)
        {
            count-=s.charAt(i-k)=='B'?1:0;
            count+=s.charAt(i)=='B'?1:0;
            ans=Math.max(ans,count);
        }
        System.out.println(k-ans);
    }
}

```

# 3.program

You are an architect tasked with designing a series of connected rooms in a

building. You are given a list of room sizes represented by an integer array

roomSizes, an integer maxFrequency representing the maximum number of times

a particular room size can appear, and an integer maxArea representing

the maximum allowable total area of connected rooms. A set of connected

rooms is called viable if the frequency of each room size in this set is

less than or equal to maxFrequency, and the total area of the rooms in

this set is less than or equal to maxArea.

Return the length of the longest viable set of connected rooms from roomSizes.

Input Format:

- ------------

Line-1: 3 space separated integers, n, maxFrequency, maxArea

Line-2: N space separated integers, roomSizes[].

Output Format:

- ------------

An integer, the length of the longest viable set of connected rooms

Sample Input-1:

- --------------

8 2 10

1 2 3 1 2 3 1 2

Sample Output-1:

- ---------------

5

Explanation:

- -----------

The longest possible viable set of connected rooms is [1, 2, 3, 1, 2] since

the room sizes 1, 2, and 3 appear at most twice, and the total area is less than 10.

Sample Input-2:

- --------------

6 1 3

1 2 1 2 1 2

Sample Output-2:

- ---------------

2

Explanation: The longest possible viable set of connected rooms is [1, 2] since

the room sizes 1 and 2 appear at most once, and the total area is 3.

Constraints:

- -----------

1 <= roomSizes.length <= 10^5

1 <= roomSizes[i] <= 10^4 where roomSizes[i] is the size of the i-th room.

1 <= maxFrequency <= roomSizes.length

1 <= maxArea <= 10^9

```java
import java.util.*;

class Solution{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n=sc.nextInt();
        int mfreq=sc.nextInt();
        int marea = sc.nextInt();
        int arr[] = new int[n];
        for(int i=0;i<n;i++){
            arr[i]=sc.nextInt();
        }
        HashMap<Integer,Integer> map = new HashMap<>();
        int len=0;
        int sum=0;
        int fin=0;
        int ind=0;
        for(int i=0;i<n;i++)
        {
            int val = arr[i];
            map.put(val, map.getOrDefault(val, 0) + 1);
            sum += val;
            while (map.get(val) > mfreq || sum > marea) {
                map.put(arr[ind], map.get(arr[ind]) - 1);
                sum -= arr[ind];
                ind++;
            }
            fin = Math.max(fin, i - ind + 1);

        }
        System.out.println(fin);

    }
}
```

## **Program4**

In a software development company, a team works on various projects over n weeks.

The team completes a certain number of tasks tasks[i] each week and dedicates

hours[i] hours of work. Given an integer k, for every consecutive sequence of

k weeks (tasks[i], tasks[i+1], ..., tasks[i+k-1] and

hours[i], hours[i+1], ..., hours[i+k-1] for all 0 <= i <= n-k),

they evaluate T, the total number of tasks completed during that sequence

of k weeks, and E, the total hours of work during that sequence of k weeks:

a) If T < lower and E >= work_goal, the team performed very poorly and loses 2 points

b) If T < lower and E < work_goal, the team performed poorly and loses 1 point.

c) If T >= upper and E >= work_goal, the team performed well and gains 1 point.

d) If T >= upper and E < work_goal, the team performed exceptionally well and gains 2 points.

e) Otherwise, the team's performance is normal and there is no change in points.

Initially, the team starts with zero points. Return the total number of points

the team has after working for n weeks. Note that the total points can be negative.

Example 1

Input:

n = 5

tasks = [10, 20, 30, 40, 50]

hours = [30, 20, 10, 30, 40]

k = 2

lower = 35

upper = 70

work_goal = 45

Output: 1

Explanation:

For [10, 20] and [30, 20]:

T = 30 < lower and E = 50 >= work_goal, the team performed very poorly and loses 2 points.

For [20, 30] and [20, 10]:

T = 50 >= lower and T <= upper and E = 30 < work_goal, no change in points.

For [30, 40] and [10, 30]:

T = 70 = upper and E = 40 < work_goal, the team performed exceptionally well and

gains 2 points.

For [40, 50] and [30, 40]:

T = 90 > upper and E = 70 >= work_goal, the team performed well and gains 1 point.

Therefore, the team gains 1 point (0 - 2 + 2 + 1 = 1).

Sample Input=

4	//n

5 8 10 15

25 30 20 25

3	//k

25	//lower

40	//upper

60	//work_goal

Sample Output=

- 2

```java
import java.util.*;

class Solution{
    static int points=0;

    static void genPoints(int T, int E, int l, int u, int wg)
    {
        if(T<l && E>=wg) points-=2;
        if(T<l && E<wg) points-=1;
        if(T>=u && E>-u) points+=1;
        if(T>=u && E<wg) points+=1;

    }
    public static void main(String[] args){
        Scanner sc=new Scanner(System.in);
        int n=sc.nextInt();
        int tasks[] = new int[n];
        int hours[] = new int[n];
        for(int i=0;i<n;i++) tasks[i]=sc.nextInt();
        for(int i=0;i<n;i++) hours[i]=sc.nextInt();
        int k=sc.nextInt();
        int l=sc.nextInt();
        int u=sc.nextInt();
        int wg=sc.nextInt();

        // int points=0;
        int T=0;
        int E=0;

        for(int i=0;i<k;i++)
        {
            T+=tasks[i];
            E+=hours[i];
        }
        genPoints(T,E,l,u,wg);
        int left=0;
        for(int r=k;r<n;r++)
        {
            T-=tasks[left];
            T+=tasks[r];
            E-=hours[left];
            E+=hours[r];
            left++;
            genPoints(T,E,l,u,wg);
        }
        System.out.println(points);

    }
}
```

## **Program5**

You are a treasure hunter exploring an ancient vault filled with

treasure boxes. The vault is represented as an array treasures of

n integers, where each integer corresponds to the value of a treasure.

You have a special key that allows you to scan and select treasures

from a sub-vault (a segment of the array) of size k. Additionally,

you have a magical power factor f and a priority filter x.

The priority-weighted treasure sum of a sub-vault is calculated as follows:

1. Count the occurrences of each treasure value in the sub-vault.

2. Assign a priority score to each treasure based on its frequency

multiplied by the treasure's value raised to the power of f

(i.e., priority_score[treasure] = frequency[treasure] * (value^f)).

3. Select only the top x treasures based on their priority scores.

If two treasures have the same priority score, the treasure with

the higher value is prioritized.

4. Calculate the total value of the selected treasures.

Your task is to return an integer array priority_sums of length n - k + 1,

where priority_sums[i] represents the priority-weighted treasure sum for

the sub-vault corresponding to treasures[i..i + k - 1].

Input Format:

- --------------

Line-1: Four space separated integers, N, K, X, F

Line-2: N space separated integers, boxes[].

Output Format:

- ----------------

An integer array, priority_sums[], of length n - k + 1

Sample Input-1:

- ----------------

8 5 2 2

1 2 3 1 2 2 3 4

Sample Output-1:

- -------------------

[7, 9, 10, 7]

Explanation:

We calculate the priority-weighted treasure sum for each sub-vault:

1. Sub-vault 1: [1, 2, 3, 1, 2]

- Frequencies: {1: 2, 2: 2, 3: 1}

- Priority scores:

- 1 → 2 * (1^2) = 2

- 2 → 2 * (2^2) = 8

- 3 → 1 * (3^2) = 9

- Top 2 treasures by priority: 3 (score 9) and 2 (score 8).

- Total value: 2 + 3 + 2  = 7.

2. Sub-vault 2: [2, 3, 1, 2, 2]

- Frequencies: {2: 3, 3: 1, 1: 1}

- Priority scores:

- 2 → 3 * (2^2) = 12

- 3 → 1 * (3^2) = 9

- 1 → 1 * (1^2) = 1

- Top 2 treasures by priority: 2 (score 12) and 3 (score 9).

- Total value: 2 + 2 + 2 + 3 = 9.

3. Sub-vault 3: [3, 1, 2, 2, 3]

- Frequencies: {3: 2, 2: 2, 1: 1}

- Priority scores:

- 3 → 2 * (3^2) = 18

- 2 → 2 * (2^2) = 8

- 1 → 1 * (1^2) = 1

- Top 2 treasures by priority: 3 (score 18) and 2 (score 8).

- Total value: 3 + 2 + 2 + 3 = 10.

4. Sub-vault 4: [1, 2, 2, 3, 4]

- Frequencies: {1: 1, 2: 2, 3: 1, 4: 1}

- Priority scores:

- 2 → 2 * (2^2) = 8

- 3 → 1 * (3^2) = 9

- 4 → 1 * (4^2) = 16

- 1 → 1 * (1^2) = 1

- Top 2 treasures by priority: 4 (score 16) and 3 (score 9).

- Total value: 3 + 4  = 7.

Sample Input-2:

- ----------------

6 3 2 1

5 5 6 7 5 6

Sample Output-1:

- -------------------

[16, 13, 13, 13]

Constraints:

1. 1 <= n == treasures.length <= 50

2. 1 <= treasures[i] <= 50

3. 1 <= x <= k <= treasures.length

4. 1 <= f <= 10

```java
import java.util.*;

class Solution{

    static PriorityQueue<int[]>  getPriorityScores(HashMap<Integer,Integer> map,int f){
        PriorityQueue<int[]> pq = new PriorityQueue<>((a,b)->b[1]-a[1]);
        for(Map.Entry<Integer,Integer> m : map.entrySet())
        {
            int ps = m.getValue()*((int)Math.pow(m.getKey(),f));
            pq.add(new int[]{m.getKey(),ps});
        }
        return pq;
    }

    static int getFinalValue(PriorityQueue<int[]> pq,HashMap<Integer,Integer> map, int x){
        int sum=0;
        for(int i=0;i<x;i++){
            int[] ps = pq.poll();
            int occ = map.get(ps[0]);
            sum+=(occ*ps[0]);
        }
        return sum;
    }
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n=sc.nextInt();
        int k=sc.nextInt();
        int x=sc.nextInt();
        int f=sc.nextInt();
        int arr[] = new int[n];
        for(int i=0;i<n;i++) arr[i]=sc.nextInt();

        HashMap<Integer,Integer> map=new HashMap<>();
        int ans[] = new int[n-k+1];
        for(int i=0;i<k;i++){
            map.put(arr[i],map.getOrDefault(arr[i],0)+1);
        }
        PriorityQueue<int[]> pq = getPriorityScores(map,f);
        int ind=0;
        ans[ind]=getFinalValue(pq,map,x);;
        ind++;
        int left=0;
        for(int i=k;i<n;i++){
            map.put(arr[left],map.get(arr[left])-1);
            left++;
            map.put(arr[i],map.getOrDefault(arr[i],0)+1);
            pq = getPriorityScores(map,f);
            ans[ind++]=getFinalValue(pq,map,x);
        }

        for(int i=0;i<ans.length;i++) System.out.print(ans[i]+" ");
    }
}
```

## **Program6**

public In a distant galaxy, there exists an ancient space station covered in a vast

array of digital codes. These codes are believed to hold the key to unlocking

powerful alien technology. The interstellar explorers call these codes "prime

sequences."

The prime-sequence beauty of the digital code is defined as the number of prime

sequences that meet the following conditions:

-The prime sequence has a length of k.

-The prime sequence is a divisor of the entire digital code.

-The prime sequence is a prime number.

Given the digital code on the space station, represented as an integer code, and

the length of the prime sequences k, return the prime-sequence beauty of the code.

Note:

- ----

Leading zeros in prime sequences are allowed.

0 is not a divisor of any value.

A prime sequence is a contiguous sequence of characters in the main digital code.

Input Format:

- ------------

Line-1: space separated String and integer, code and K

Output Format:

- ------------

An integer, the prime-sequence beauty of the code.

Sample Input:

- ------------

239246 2

Sample Output:

- -------------

1

Explanation:

- -----------

The following are the prime sequences of length k:

"23" from "239246": 23 is a divisor of 239246 and is a prime number.

"39" from "239246": 39 is not a divisor.

"92" from "239246": 92 is not a divisor.

"24" from "239246": 24 is is not a divisor 239246.

"46" from "239246": 46 is a divisor of 239246 but is not a prime number.

Therefore, the prime-sequence beauty is 1.

Sample Input:

- ------------

24224 1

Sample Output:

- -------------

3

{

}

```java
import java.util.*;

class Solution{
    static int c=0;

    static boolean validate(StringBuilder s, long n)
    {
        String s1=s.toString();
        if(n%Long.parseLong(s1)!=0) return false;
        Long num=Long.parseLong(s1);
        if(num==1 || num==0) return false;
        for(int i=2;i*i<=num;i++)
        {
            if(num%i==0) return false;
        }
        return true;
    }
    static void primeSeq(int[] arr, int k, long n)
    {
        StringBuilder s=new StringBuilder();
        for(int i=0;i<k;i++)
        {
            s.append(arr[i]);
        }
        if(validate(s,n))
        {
            c++;
        }
        for(int i=k;i<arr.length;i++)
        {
            s.deleteCharAt(0);
            s.append(arr[i]);
            if(validate(s,n)) c++;
        }
    }
    public static void main (String[] args) {
        Scanner sc = new Scanner(System.in);
        long n=sc.nextInt();
        int k=sc.nextInt();
        String s=n+"";
        int arr[] = new int[s.length()];
        for(int i=0;i<s.length();i++){
            arr[i]=Integer.parseInt(s.charAt(i)+"");
        }
        primeSeq(arr,k,n);
        System.out.println(c);
    }
}

```

## **Program7**

In a film festival, there is a lineup of movies, each with a rating. The festival

organizer wants to find the maximum total rating of 'k' sequence of movies while

following these rules:

1. The sequence must be exactly k movies long.

2. Each movie in the sequence must have a distinct rating.

3. None of the movies in the sequence should have a restricted rating, as

these are reserved for special screenings.

Given an array movieRatings representing the sequence of movie ratings, an integer k

representing the length of the sequence, and a set restrictedRatings (of size m) of

special ratings, find the maximum total rating of any valid sequence.

If no valid sequence exists, return -1.

Input Format:

- ------------

Line-1: 3 space separated integers, n, k, m

Line-2: n space separated integers, movieRatings[].

Line-3: m space separated integers, restrictedRatings[].

Output Format:

- ------------

An integer, the maximum total rating of any valid sequence

Sample Input-1:

- --------------

7 3 2

1 5 4 2 9 9 9

2 9

Sample Output-1:

- ---------------

10

Explanation:

- -----------

The sequences of movie ratings with length 3 are:

- [1, 5, 4] which meets the requirements and has a total rating of 10.
- [5, 4, 2] which does not meet the requirements because 2 is in the

restricted set.

- [4, 2, 9] which does not meet the requirements because 2 and 9 are in

the restricted set.

- [2, 9, 9] which does not meet the requirements because 2 and 9 are in

the restricted set and 9 is repeated.

- [9, 9, 9] which does not meet the requirements because 9 is in

the restricted set and repeated.

We return 10 because it is the maximum total rating of all the sequences

that meet the conditions.

Sample Input-2:

- --------------

3 3 1

4 4 4

4

Sample Output-2:

- ---------------
- 1

Explanation: The sequences of movie ratings with length 3 are:

[4, 4, 4] which does not meet the requirements because 4 is repeated and in the restricted set.

We return -1 because no sequences meet the conditions.

Constraints:

- -----------

0 <= m <= n <=1000

k <= n

0 ≤ restrictedRatings.length ≤ 1000

```java
import java.util.*;

class Solution{

    static int c=0;
    static boolean f=false;
    static boolean valid(ArrayList<Integer> temp,ArrayList<Integer> res)
    {
        // System.out.println(temp);
        HashSet<Integer> set = new HashSet<>();
        for(int i=0;i<temp.size();i++)
        {
            if(set.contains(temp.get(i)) || res.contains(temp.get(i)))
            {
                return false;
            }
            else{
                set.add(temp.get(i));
            }
        }
        return true;
    }
    static void check(int[] arr,ArrayList<Integer> res,int k)
    {
        ArrayList<Integer> temp=new ArrayList<>();
        // boolean valid=true;
        for(int i=0;i<k;i++)
        {
            temp.add(arr[i]);
        }
        if(valid(temp,res))
        {
            int sum=0;
            for(int i=0;i<temp.size();i++) sum+=temp.get(i);
            c=Math.max(c,sum);
            f=true;
        }

        for(int i=k;i<arr.length;i++){
            temp.remove(0);
            temp.add(arr[i]);
            if(valid(temp,res))
            {
                int sum=0;
                for(int j=0;j<temp.size();j++) sum+=temp.get(j);
                c=Math.max(c,sum);
                f=true;
            }
        }

    }
    public static void main (String[] args) {
        Scanner sc = new Scanner(System.in);
        int n=sc.nextInt();
        int k=sc.nextInt();
        int m=sc.nextInt();
        int ratings[] = new int[n];
        for(int i=0;i<n;i++) ratings[i]=sc.nextInt();

        ArrayList<Integer> res = new ArrayList<>();
        for(int i=0;i<m;i++) res.add(sc.nextInt());

        check(ratings,res,k);

        System.out.println(f?c:-1);

    }
}
```

## **Program8**

You are given an integer array nums and two integers l and r. Your task is to

analyze the volatility of a sequence of values. The volatility of a sequence is

defined as the difference between the maximum and minimum values in that sequence.

You need to determine the sequence with the highest volatility among all

sequences of length between l and r (inclusive).

Return the highest volatility. If no such sequence exists, return -1.

Input Format:

- ------------

Line-1: 3 space separated integers, n, l, r

Line-2: n space separated integers, nums[].

Output Format:

- ------------

An integer, the highest volatility.

Sample Input-1:

- --------------

5 2 3

8 3 1 6 2

Sample Output-1:

- ---------------

7

Explanation:

- -----------

The possible sequences of length between l = 2 and r = 3 are:

[8, 3] with a volatility of 8−3=5

[3, 1] with a volatility of 3−1=2

[1, 6] with a volatility of 6−1=5

[8, 3, 1] with a volatility of 8−1=7

The sequence [8, 3, 1] has the highest volatility of 7.

Sample Input-2:

- --------------

4 2 4

5 5 5 5

Sample Output-2:

- ---------------

0

Explanation:

- -----------

All possible sequences have no volatility as the maximum and minimum values

are the same, resulting in a difference of 0.

```java
import java.util.*;

class Solution{

    static int c=-1;
    static void find(int[] arr, int k)
    {
        int max=arr[0];
        int min=arr[0];
        TreeSet<Integer> temp=new TreeSet<>();
        for(int i=0;i<k;i++)
        {
            temp.add(arr[i]);
        }
        c=Math.max(c,temp.last()-temp.first());
        for(int i=k;i<arr.length;i++)
        {
            temp.remove(arr[i-k]);
            temp.add(arr[i]);
            c=Math.max(c,temp.last()-temp.first());
        }
    }
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n= sc.nextInt();
        int l= sc.nextInt();
        int r= sc.nextInt();
        int arr[] = new int[n];

        for(int i=0;i<n;i++) arr[i]=sc.nextInt();

        find(arr,r);

        System.out.println(c);

    }
}
```

## **Program9**

public You are an architect designing a street with houses represented as a 0-indexed array

house_heights of n integers, where each element represents the height of a house.

Additionally, a binary array visibility_mask of length n is provided, where 1 indicates

a house that contributes to the neighborhood's skyline, and 0 indicates a house that does not.

For any house located at index i, you are tasked with determining the average

skyline height within a k-radius neighborhood centered at i. The average skyline

height is the average of all house heights between indices i - k and i + k (inclusive)

that have a corresponding visibility value of 1 in the visibility_mask.

If no houses with a visibility of 1 exist in the range, or if the range extends

beyond the boundaries of the array, the average skyline height for that house is -1.

Return an array skyline_avgs of length n, where skyline_avgs[i] is the average

skyline height for the neighborhood centered at index i.

Example 1:

Input:

house_heights = [10, 15, 20, 5, 30, 25, 40]

visibility_mask = [1, 0, 1, 1, 0, 1, 1]

k = 2

Output:

skyline_avgs = [-1, -1, 11, 16, 22, -1, -1]

Explanation:

- For index 0, there are less than k houses in the left neighborhood,

so skyline_avgs[0] = -1.

- For index 1, there are less than k houses in the left neighborhood,

so skyline_avgs[1] = -1.

- For index 2, the neighborhood is [10, 15, 20, 5, 30]. From the visibility_mask,

only the houses with heights [10, 20, 5] contribute to the skyline. The average

is (10 + 20 + 5) / 3 = 11.

- For index 3, the neighborhood is [15, 20, 5, 30, 25]. From the visibility_mask,

only the houses with heights [20, 5, 25] contribute.

The average is (20 + 5 + 25) / 3 = 16.

- For index 4, the neighborhood is [20, 5, 30, 25, 40]. From the visibility_mask,

only the houses with heights [20, 5, 25, 40] contribute. The average

is (20 + 5 + 25 + 40) / 4 = 22.

- For index 5, there are less than k houses in the right neighborhood,

so skyline_avgs[5] = -1.

- For index 6, there are less than k houses in the right neighborhood,

so skyline_avgs[6] = -1.

Sample Input:

3

1

50 60 70

1 1 1

Sample Output:

[-1, 60, -1]

Constraints:

1. n == house_heights.length == visibility_mask.length

2. 1 <= n <= 10^5

3. 0 <= house_heights[i] <= 10^5

4. visibility_mask[i] is either 0 or 1

5. 0 <= k <= n

{

}

```java
import java.util.*;

class Solution{
    static ArrayList<Integer> ans;
    static void solve(int n, int k, int[] h,int []b){
        int sum=0;
        int c=0;

        if(2*k+1>n)
        {
          for(int i=0;i<n;i++) ans.add(-1);
        }
        else
        {
            for(int i=0;i<k;i++) ans.add(-1);
            for(int i=0;i<2*k+1;i++)
            {
                if(b[i]==1) {sum+=h[i];c++;}

            }
            ans.add(sum/c);
            for(int i=k+1;i<n-k;i++)
            {
                if(b[i+k]==1)
                {
                    sum+=h[i+k];
                    c++;
                }
                if(b[i-k-1]==1)
                {
                    sum-=h[i-k-1];
                    c--;
                }
                ans.add(sum/c);
            }
            for(int i=n-k;i<n;i++) ans.add(-1);
        }
    }
    public static void main (String[] args) {
        Scanner sc = new Scanner(System.in);
        int n=sc.nextInt();
        int k=sc.nextInt();
        int h[] = new int[n];
        for(int i=0;i<n;i++) h[i]=sc.nextInt();
        int b[] = new int[n];
        for(int i=0;i<n;i++) b[i]=sc.nextInt();
        ans = new ArrayList<>();

        solve(n,k,h,b);

        System.out.println(ans);

    }
}
```

## **Program10**

public You are a renowned Alchemist exploring a mystical forest teeming with magical plants.

Each plant you encounter has a unique Essence Power represented by an integer in

the array plants of length n.

By collecting essences from consecutive plants, you can brew powerful Elixirs.

The potency of an elixir is determined by the sum of the essence powers of the plants used.

Due to the complexity of brewing, you can only create elixirs using sequences of

plants that are at least m in length.

Your objective is to find the kth smallest elixir potency that can be brewed

from these sequences.

Example 1:

Input: n=3 plants = [2, 1, 3], k = 2, m = 2

Output: 4

Explanation:

Possible elixirs (sequences of length ≥ 2):

- [2, 1]: Potency = 2 + 1 = 3
- [1, 3]: Potency = 1 + 3 = 4
- [2, 1, 3]: Potency = 2 + 1 + 3 = 6

Ordered elixir potencies: 3, 4, 6

The 2nd smallest elixir potency is 4.

Input Format:

- ------------

Line-1: 3 space separated integers, n, k, m

Line-2: n space separated integers, movieRatings[].

Output Format:

- ------------

An integer, The kth smallest elixir potency

Sample Input:

4 3 2

3 -3 5 2

Sample output:

4

Explanation:

Possible elixirs (sequences of length ≥ 2):

- [3, -3]: Potency = 3 + -3 = 0
- [-3, 5]: Potency = -3 + 5 = 2
- [5, 2]: Potency = 5 + 2 = 7
- [3, -3, 5]: Potency = 3 + -3 + 5 = 5
- [-3, 5, 2]: Potency = -3 + 5 + 2 = 4
- [3, -3, 5, 2]: Potency = 3 + -3 + 5 + 2 =7

Ordered elixir potencies: 0, 2, 4, 5, 7, 7

The 3rd smallest elixir potency is 4. {

}

```java
import java.util.*;

class Solution{
    static PriorityQueue<Integer> q;
    static void helper(int[] p,int k)
    {
        int sum=0;
        for(int i=0;i<k;i++)
        {
            sum+=p[i];
        }
        q.add(sum);
        for(int i=k;i<p.length;i++){
            sum-=p[i-k];
            sum+=p[i];
            q.add(sum);
        }
    }
    static int solve(int n, int k, int m,int[] p){
        q = new PriorityQueue<>();
        for(int i=m;i<=n;i++)
        {
            helper(p,i);
        }

        for(int i=0;i<k-1;i++) q.poll();

        return q.poll();
    }
    public static void main (String[] args) {
        Scanner sc = new Scanner(System.in);
        int n=sc.nextInt();
        int k=sc.nextInt();
        int m=sc.nextInt();
        int p[] =  new int[n];
        for(int i=0;i<n;i++) p[i]=sc.nextInt();

        System.out.print(solve(n,k,m,p));
    }
}
```