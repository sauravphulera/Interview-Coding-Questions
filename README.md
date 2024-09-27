# Interview Coding Questions

## 1.Majority Element
Given an array <code>nums</code> of size <code>n</code>, return the majority element.

The majority element is the element that appears more than <code>⌊n / 2⌋</code> times. You may assume that the majority element always exists in the array.
  ### Solution
  ### Approach 1: Sorting
  Intuition:
  The intuition behind this approach is that if an element occurs more than n/2 times in the array (where n is the size of the array), it will always occupy the middle position when the array is sorted. Therefore, we can sort the array and    return the element at index n/2.
  
  ### Explanation:
  The code begins by sorting the array nums in non-decreasing order using the sort function from the C++ Standard Library. This rearranges the elements such that identical elements are grouped together.
  Once the array is sorted, the majority element will always be present at index n/2, where n is the size of the array.
  This is because the majority element occurs more than n/2 times, and when the array is sorted, it will occupy the middle position.
  The code returns the element at index n/2 as the majority element.
  The time complexity of this approach is O(n log n) since sorting an array of size n takes O(n log n) time.
  
  ### Approach 2: Hash Map
  ### Intuition:
  The intuition behind using a hash map is to count the occurrences of each element in the array and then identify the element that occurs more than n/2 times. By storing the counts in a hash map, we can efficiently keep track of the       
  occurrences of each element.

  ### Approach 3: Moore Voting Algorithm
  #### Time Complexity: <code>O(n)</code>, Space: <code>O(0)</code>
  Intuition:
  The intuition behind the Moore's Voting Algorithm is based on the fact that if there is a majority element in an array, it will always remain in the lead, even after encountering other elements.
  ### Algorithm:
  Initialize two variables: count and candidate. Set count to 0 and candidate to an arbitrary value.
  Iterate through the array nums:
  a. If count is 0, assign the current element as the new candidate and increment count by 1.
  b. If the current element is the same as the candidate, increment count by 1.
  c. If the current element is different from the candidate, decrement count by 1.
  After the iteration, the candidate variable will hold the majority element.

  ```javascript
     majorityElement(nums) {
        let count = 0;
        let candidate = 0;
        
        for (let num of nums) {
            if (count == 0) {
                candidate = num;
            }
            
            if (num == candidate) {
                count++;
            } else {
                count--;
            }
        }
        
        return candidate;
    }
  ```
## 2. Best Time to Buy and Sell Stock II (buy and sell multiple times)
### Problem Statement
You are given an integer array prices where prices[i] is the price of a given stock on the ith day.
On each day, you may decide to buy and/or sell the stock. You can only hold at most one share of the stock at any time. However, you can buy it then immediately sell it on the same day.
Find and return the maximum profit you can achieve.

### Solution
[Video Explanation](https://youtu.be/LTnycd5PzDg)
Let's think about this case. We have a descreasing part.

<code>Input: prices = [1,5,3,100]</code>.
In this case, 100 - 1 = 99 is the maximum profit? It's not. The maximum profit should be 101.
<code>
buy a stock with `1`
sell a stock with `5` (= profit 4)
buy a stock with `3`
sell a stock with `100` (= profit 97 + 4)
= 101
</code>
<b> Note: Given the consideration of taking the maximum profit from the two cases, Seems like we should sell a stock immediately when we find larger number, because we got maximum profit in the both cases. </b>
Time complexity: <code>O(n)</code>
Space complexity:<code> O(1) </code>

```javascript
var maxProfit = function(prices) {
    let profit = 0;
    for(let i=1;i<prices.length;i++) {
        if(prices[i] > prices[i-1]) {
            profit += prices[i] - prices[i-1];
        }
    }
    return profit;
};
```

## 3.Rotate an Array

Given an integer array nums, rotate the array to the right by k steps, where k is non-negative.

### Approach 1 Time complexity (k*n) n is for shift operation ans Space is O(0).
The Idea is simple yoy have <code>[1,2,3,4,5]</code> and <code>k=2</code>. The result will be <code>[4,5,1,2,3]</code> so the last 2 elements are appended to first. So we will just fetch last elements from <code>n-k to n</code> and append them to the start of array at the same time.
```javascript
  var rotate = function(nums, k) {
      let n = nums.length;
      if(k == 0) return nums;
      for(let i=nums.length -1; i >= n-k; i--) {
          const temp = nums.pop();
          nums.unshift(temp);
      }
      return nums;
  };
```
### Better Approach O(n)
For <code>[1,2,3,4,5]</code> and <code>k=2</code>
1. The entire array is reversed from index <code>0 to len(nums) - 1</code>.
   This step places the elements that need to be rotated to the front. <code>[5,4,3,2,1]</code>
2. Reverse the First k Elements: <code>[4,5,3,2,1]</code>
3. Reverse the remaining <code>n-k</code> elements. <code>[4,5,1,2,3] </code>
```javascript
  var rotate = function(nums, k) {
      let n = nums.length;
      k = k % n; // handle cases where k >= n
      if(k == 0) return nums;
  
          // Reverse the entire array
          nums.reverse();
          console.log(nums)
          // Reverse the first k elements
          reverseBetween(nums,0, k-1);
          // Reverse the remaining elements (from k to end)
          reverseBetween(nums,k, n-1);
  
      return nums;
  };
```

## 4. Jump Game
You are given an integer array nums. You are initially positioned at the array's first index, and each element in the array represents your maximum jump length at that position.
Return true if you can reach the last index, or false otherwise.
Example 1:

Input: nums = <code>[2,3,1,1,4]</code>    
Output: true  
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.  

Example 2:
Input: nums = <code>[3,2,1,0,4]</code>  
Output: false  
Explanation: You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index.  

**Simplest Approach O(n) and Space O(1)**
Imagine you have a car, and you have some distance to travel (the length of the array). This car has some amount of gasoline, and as long as it has gasoline, it can keep traveling on this road (the array). Every time we move up one element in the array, we subtract one unit of gasoline. However, every time we find an amount of gasoline that is greater than our current amount, we "gas up" our car by replacing our current amount of gasoline with this new amount. We keep repeating this process until we either run out of gasoline (and return false), or we reach the end with just enough gasoline (or more to spare), in which case we return true.
**Note**: We can let our gas tank get to zero as long as we are able to gas up at that immediate location (element in the array) that our car is currently at.
```javascript
var canJump = function(nums) {
    let gas = 0;
    for(let num of nums) {
        if(gas < 0) return false;
        if(gas < num) {
            gas = num;
        } 
        gas--;
    }

    return true;
};
```

## 5. Jump Game 2
**You are given a 0-indexed array of integers nums of length n. You are initially positioned at nums[0].**

Each element nums[i] represents the maximum length of a forward jump from index i. In other words, if you are at nums[i], you can jump to any nums[i + j] where:

0 <= j <= nums[i] and  
i + j < n  
Return the minimum number of jumps to reach nums[n - 1]. The test cases are generated such that you can reach nums[n - 1].

 

**Example 1:**

Input: nums = [2,3,1,1,4]  
Output: 2  
Explanation: The minimum number of jumps to reach the last index is 2. Jump 1 step from index 0 to 1, then 3 steps to the last index.  

**Solution O(n)**
You just have to keep finding the farthest position you can reach from i <code>for i =0 farthest = i + nums[i] = 2</code> and then untill you reach that farthest position <code>ie i == 2</code> find the next farthest position <code>ie max(farthest, i+nums[i])</code>. whenever you reach a farthest position increase your jump count.  

**Steps:**

**Track the Farther:** As I move through the array, I keep track of the farthest index I can reach.

**Jump When Needed:** When I reach the end of the current jump range, I make a jump and update the end of the range to the farthest point I calculated.

```javascript
var jump = function(nums) {

    let farthest = 0, end = 0, jump = 0;
    for(let i=0; i < nums.length - 1; i++) {
        farthest = Math.max(farthest, i+ nums[i]);

        if(i == end) {
            end = farthest;
            jump++;
        }
    }
    return jump
};
```
## 6. H-Index
Given an array of integers citations where citations[i] is the number of citations a researcher received for their ith paper, return the researcher's h-index.

According to the definition of h-index on Wikipedia: The h-index is defined as the maximum value of h such that the given researcher has published at least h papers that have each been cited at least h times.
Example 1:

Input: citations = [3,0,6,1,5]  
Output: 3  
Explanation: [3,0,6,1,5] means the researcher has 5 papers in total and each of them had received 3, 0, 6, 1, 5 citations respectively.  
Since the researcher has 3 papers with at least 3 citations each and the remaining two with no more than 3 citations each, their h-index is 3.  

### Approach: 1 Sorting and Iteration O(nlogn)
**Sorting**: Sorts the citations list in ascending order.
Iterative Check: Iterates through the sorted list.  
For each citation v at index i:  
If n - i (number of articles with at least n - i citations) is less than or equal to v itself (the current citation count), it means the h-index is n - i.  
Returns n - i as the h-index.  
Default Return: If no valid h-index is found, returns 0.  
```javascript
var hIndex = function(a) {
    if(a.length == 1) {
        return a[0] == 0 ? 0 : 1;
    }
    a.sort((a,b) => b-a)

    let h = a.length;
    while(h > 0) {
        if(a[h-1] >= h) {
            return h;
        }
        h--;
    } 
    return h;
};
```
### Approach: 2 Counting Frequency and Backward Iteration
**Frequency Array**: Creates a temporary array temp of size n + 1 to store citation frequencies.  
**Counting Citations**: Iterates through the citations list:  
If a citation v is greater than n, adds it to the highest frequency bucket (temp[n]).  
Otherwise, increments the count in the corresponding bucket (temp[v]).  
Calculating h-index: Iterates backward through the temp array:  
Accumulates the total number of citations up to each index i.  
If the total count (total) is greater than or equal to i itself, it means i is the h-index.  
Returns i as the h-index.  
```javascript
function hIndex(citations) {
    const n = citations.length;
    const temp = new Array(n + 1).fill(0);

    for (let i = 0; i < citations.length; i++) {
        const v = citations[i];
        if (v > n) {
            temp[n] += 1;
        } else {
            temp[v] += 1;
        }
    }

    let total = 0;
    for (let i = n; i >= 0; i--) {
        total += temp[i];
        if (total >= i) {
            return i;
        }
    }
}
```

## Product of array except self
Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].  

The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.  

You must write an algorithm that runs in O(n) time and without using the division operation.  

 

Example 1:  

Input: nums = <code>[1,2,3,4]</code>
Output: <code>[24,12,8,6]</code>
Example 2:

Input: nums = <code>[-1,1,0,-3,3]</code>
Output: <code>[0,0,9,0,0]</code>

**1. Dividing the product of array with the number**
What we would do is, we would find the product of all the numbers of our Array and then divide the product with each element of the array to get the new element for that position in our final answer array.

Now after presenting the interviewer with this solution, here is our one more chance to shine out in the interview. We would specifically tell the interviewer that one major con in going with this method is when we have an element as 0 in our array. The problem is that, we can't perform a division by 0, as a result, we won't be able to get corresponding values in our final answer array for the indices having <code>0</code> in our initial array at that position.

**2. Solution O (n)**
Calculate left products in left array  
Calculate right products in right subarray  
get result with product of both left and right

```javascript
var productExceptSelf = function(nums) {
    let left = [], right = [], res = [];
    const n =nums.length;

    // calc left products
    for(let i=0; i < nums.length; i++) {
        if(i === 0) {
            left[i] = 1;
        } else {
            left[i] = nums[i-1] * left[i-1];
        }
    }

    // calc right products
    for(let i=n-1; i >=0; i--) {
        if(i == n-1){
            right[i] = 1;
        } else {
            right[i] = right[i+1] * nums[i+1]
        }
    }

    for(let i= 0; i< n;i++) {
        res[i] = left[i] * right[i];
    }

    return res;
};
```
