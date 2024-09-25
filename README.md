# Interview Coding Questions

## Majority Element
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

