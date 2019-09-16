# Chapter 04: Data Structure I - Sequence

## Topic 1: **Sorted List**

Requirement: Approach the problem with both bottom-up and top-down algorithms. You will be expected to know the complexity of an algorithm and how you can improve/change it. Algorithms that are used to solve  problems include sorting (plus searching and binary search), divide-and-conquer, dynamic programming/memoization, greediness, recursion or algorithms linked to a specific data structure. Know Big-O notations (e.g. run time) and be ready to discuss complex algorithms like Dijkstra and A*. We recommend discussing or outlining the algorithm you have in mind before writing code. You should know the details of at least one n*log(n) sorting algorithm, preferably two (e.g. quicksort and merge sort ). Merge sort can be highly useful in situations where quicksort is impractical.  

### 1.1 **Binary Search**

**Binary Search Template - Search for a number**  

<pre id="VCCACAQ91Z8">def binary_search(self, nums, target):      
    if len(nums) == 0:  
        return -1  
    **start****, end** = 0, len(nums) - 1  
    <u>_**while start < end - 1:**_</u>  
        <u>_**mid** _</u><u>_**= (start + end) / 2**_</u>  
        if target > nums[mid]:  
            <u>_**start** _</u><u>_**= mid**_</u>  
        else:  
            <u>_**end =**_</u><u>_ **mid**_</u>    
    if nums[start] == target:  
        return start  
    if nums[end] == target:  
        return end  
    return -1  

    # Returns index of x in arr if present, else -1   
def binarySearch (arr, l, r, x):  
    # Check base case   
    if r >= l:   
        mid = (r + l) // 2  

        # If element is present at the middle itself   
        if arr[mid] == x:   
            return mid   

        # If element is smaller than mid, then it    
        # can only be present in left subarray   
        elif arr[mid] > x:   
            return binarySearch(arr, l, mid-1, x)   

        # Else the element can only be present    
        # in right subarray   
        else:   
            return binarySearch(arr, mid+1, r, x)   

    else:   
        # Element is not present in the array   
        return -1  

# Test array   
arr = [ 2, 3, 4, 10, 40 ]   
x = 10  

# Function call   
result = binarySearch(arr, 0, len(arr)-1, x)   

if result != -1:   
    print "Element is present at index %d" % result   
else:   
    print "Element is not present in array"</pre>

知识点  
1\. 二分位置 之 OOXX: 一般会给你一个数组. 让你找数组中第一个/最后一个满足某个条件的位置.  
2\. 二分位置 之 Half half: 并无法找到一个数组，形成 OOXX 的模型。  
     但可以根据判断，保留下有解的那一半或者去掉无解的一半.  

**Example: Find Minimum in Rotated Sorted Array II**  
Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.  
(i.e., `[0,1,2,4,5,6,7]` might become `[4,5,6,7,0,1,2]`).  
Find the minimum element.  
The array may contain duplicates.  

<pre id="VCCACAOKvd8">class Solution(object):  
    def findMin(self, n MNMums):  
        """  
        :type nums: List[int]  
        :rtype: int  
        [6,7,0,1,2,4,5]  
        [4,5,6,7,0,1,2]  
        [2,4,5,6,7,0,1]  

        Special Case: [3,3,3,3,3,3,3,3,1,3]  
        """  
        if not nums: return None  
        i = 0  
        j = len(nums) - 1  
        while i < j - 1:  
            mid = (i + j) // 2  
            if nums[mid] <= nums[mid + 1] < nums[j]  
                    or nums[mid] < nums[mid + 1] <= nums[j]:  
                j = mid  
            elif nums[mid] != nums[j]:  
                i = mid  
            else:  
                return min(nums[i:j+1])  
        return min(nums[i], nums[j])</pre>

### **1.2 2-Sum / 3-Sum**

**2-Sum Left Right Template **- Search for a sum****  
Given an array of sorted integers, return indices of the two numbers such that they add up to a specific target. You may assume that each input would have exactly one solution, and you may not use the same element twice.  

<pre id="VCCACAzXuBV">class App:  
    def twoSum(self, nums, target):   
        #rtype: List[int] -- two indexes  
        left, right = 0, len(nums) - 1  
        <u>_**while left < right:**_</u>  
            <u>_**cur_sum** _</u><u>_**= nums[left] + nums[right]**_</u>  
            if cur_sum < target:  
                left  += 1  
            elif cur_sum > target:  
                right -= 1  
            else:  
                return left, right  
        return -1</pre>

Related: 3Sum Smaller  
Given an array of n integers nums and a target, find the number of index triplets i, j, k with 0 <= i < j < k < n that satisfy the condition nums[i] + nums[j] + nums[k] < target  

<pre id="VCCACAVIUAL">class App(object):  
    def threeSumSmaller(self, nums, target):  
        nums = sorted(nums)  
        result = 0  
        for i, n in enumerate(nums):  
            subtarget = target - n  
            _<u>left  </u>__<u>= i + 1</u>_  
            # meaning: everything between i (exclusive) and left (exclusive) are satisfying   
            #    nums[left] + nums[right] < subtarget  
            _<u>right</u> __<u>= len(nums) - 1</u>_  
            <u>_**while left < right:**_</u>  
                if nums[left] + nums[right] < subtarget:  
                    **<u>_result_ </u>****<u>_+= right - left_</u>**  
                    left += 1  
                else:  
                    right -= 1  
        return result  

    def threeSumSmallerInnerWhile(self, nums, target):  
        nums = sorted(nums)  
        result = 0  
        for i, n in enumerate(nums):  
            subtarget = target - n  
            _<u>left  </u>__<u>= i + 1</u>_  
            # meaning: everything between i (exclusive) and left (exclusive) are satisfying   
            #    nums[left] + nums[right] < subtarget  
            _<u>right</u> __<u>= len(nums) - 1</u>_  
            while left < right:  
                `_<u>**while left < right** </u>_and` nums[left] + nums[right] < subtarget:   
                    # must have while left < right!!!!  
                    **<u>_result_ </u>****<u>_+= right - left_</u>**  
                    left += 1  
                right -= 1  
        return result</pre>

Related: Two Sum for general unsorted array  

<pre id="VCCACA2k2hx">class App:kIolioiu </pre>

   def twoSum(self, nums, target): #rtype: List[int] -- two indexes  
        nums = [(v, i) for i, v in enumerate(nums)]  
        nums = sorted(nums, key = lambda x: x[0])  
        left, right = 0, len(nums) - 1  
        while left < right:  
            cur_sum = nums[left][0] + nums[right][0]  
            if cur_sum < target:  
                left  += 1  
            elif cur_sum > target:  
                right -= 1  
            else:  
                return nums[left][1], nums[right][1]  
        return -1  

<pre id="VCCACAmo8Os"># Two Sum III - Data structure design  
class TwoSum:  
    def __init__(self):  
        self.uni_nums = set()  
        self.dup_nums = set()  

    def add(self, number):  
        """  
        Add the number to an internal data structure..  
        :type nnb , umber: int  
        :rtype: void  

        """  
        if number not in self.uni_nums:  
            self.uni_nums.add(number)  
        else:  
            if number not in self.dup_nums:  
                self.dup_nums.add(number)  

    def find(self, value):  
        """  
        Find if there exists any pair of numbers which sum is equal to the value.  
        :type value: int  
        :rtype: bool  
        """  
        if value / 2 in self.dup_nums:  
            return True  
        else:  
            for number in self.uni_nums:  
                if value - number in self.uni_nums and number != value - number:  
                    return True  
            return False</pre>

3-SUM: Given an array nums of n integers, are there elements a, b, c in nums such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.  

<pre id="VCCACAcvHW4">class App(object):  
    def twoSum(self, nums, first_num, start, end, results):  
        target = 0 - first_num  
        left, right = start, end  
        while left < right:  
            cur_sum = nums[left] + nums[right]  
            if cur_sum < target:  
                left  += 1  
            elif cur_sum > target:  
                right -= 1  
            else:  
                results.append([first_num, nums[left], nums[right]])  
                while left < right and nums[left + 1] == nums[left]:  
                    left += 1  
                left += 1  

    def threeSum(self, nums):  
        results = []  
        nums.sort()  
        for i, num in enumerate(nums):  
            if i > 0 and num == nums[i - 1]:  
                continue  
            self.twoSum(nums, num, i + 1, len(nums) - 1, results)  
        return results</pre>

3-SUM Follow-up — Get all possible results  

<pre id="VCCACAXvpgl">#3sum，但是一个数可以加它本身  
public List<List<Integer>> threeSum(int[] nums,int target) {  
        List<List<Integer>> res = new ArrayList<>();  
        Arrays.sort(nums);  
        for (int i = 0 ; i < nums.length; i++) {  
            if (i != 0 && nums == nums[i - 1]) continue;  
            int left = i ;  
            int right = nums.length - 1;  
            while (left <= right){  
            if (nums + nums[left] + nums[right] == target) {  
                res.add(Arrays.asList(nums,nums[left++] , nums[right--]));  
                while(left <= right &&nums[left] == nums[left - 1]) left ++;  
                while(left <= right && nums[right] == nums[right + 1]) right --;      
            }  
        else if (nums + nums[left] + nums[right] < target)  
            left ++;  
        else  
            right--;  
       }  
    }     
     return res;  
}</pre>

### **1.3 Sorting**

Merge Sort 比较stable, worst case 不需要shuffle也是o(nlogn)  

Example: Car Fleet  
`N` cars are going to the same destination along a one lane road. The destination is `target` miles away.  
Each car `i` has a constant speed `speed[i]` (in miles per hour), and initial position `position[i]` miles towards the target along the road.  
A car can never pass another car ahead of it, but it can catch up to it, and drive bumper to bumper at the same speed.  
The distance between these two cars is ignored - they are assumed to have the same position.  
A _car fleet_ is some non-empty set of cars driving at the same position and same speed. Note that a single car is also a car fleet.  
If a car catches up to a car fleet right at the destination point, it will still be considered as one car fleet.  

How many car fleets will arrive at the destination?  

<pre id="VCCACAm06yI">**Input:** target = 12, position = [10,8,0,5,3], speed = [2,4,1,1,3]  
**Output:** 3  
**Explanation**:  
The cars starting at 10 and 8 become a fleet, meeting each other at 12.  
The car starting at 0 doesn't catch up to any other car, so it is a fleet by itself.  
The cars starting at 5 and 3 become a fleet, meeting each other at 6.  
Note that no other cars meet these fleets before the destination, so the answer is 3.</pre>

<pre id="VCCACAgDTUE">class Solution:  
    def carFleet(self, target, position, speed):  
        """  
        :type target: int  
        :type position: List[int]  
        :type speed: List[int]  
        :rtype: int  
        """  
        c = sorted(zip(position, speed), reverse=True)  
        # [10,8,5,3,0], speed = [2,4,1,3,1]  
        if not position: return 0  
        count_fleet = 1  
        prev = 0  
        i = 1  
        while i < len(c):  
            # speed cannot be zero!  
            while i < len(c) and (target - c[prev][0])  
                                    / c[prev][1] >= (target - c[i][0])  / c[i][1]:  
                i += 1  
            if i < len(c):  
                count_fleet += 1  
                prev = i  
            i += 1  
        return count_fleet</pre>

Reflection: does my idea correct? Is there any case in violation to my idea?  

## Topic 2: **Unsorted List**

### **2.1 **Quick Select****

**Quick Select Template --- Kth Smallest Element in an Array by **O(n) — from ranking to number****  

Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element. For example, given [3,2,1,5,6,4] and k = 2, return 5.  
Note: You may assume k is always valid, 1 ≤ k ≤ array's length.  

# O(n) expected run time/ O(N^2) worst case running time + O(1) memory  
# If the array is shuffled, O(n) is guaranteed  

Worst-case performance‎: ‎О(n^2), Average performance‎: ‎O(n) By master theorem, Best-case performance‎: ‎О(n)  
T(n) = cn + T(n/2). Average Time Complexity is reached by Master Theorem.  As in quick sort, we have to do partition in halves (Half is used for convenience, the actual partition is not exact 50%. use Random Number),  

<div data-section-style="11" style="max-width:100%">![](https://quip.com/blob/VCCAAAgSiOv/x4WA4oxye_fO8IOqzElETw?a=KMPAv0fE9leqfZSceYAEN601OzdtM3ffnKhfaA990i8a)</div>

quickSelect(self, nums, start, end, k):  
where k is the k-th smallest element to find its value.  
pivot = nums[start]  
left, right =  
    partition(nums, start, end, pivot)  

right - left can be neighbors   
or right - pivot_value - left  

All the elements with index <= right are <= right-th element in the sorted array  

All the elements with index >= left are <= left-th element in the sorted array  

<pre id="VCCACAsMl0z">class App(object):  
    def findKthLargest(self, nums, k):  
        if not nums: return None  
        return self.quickSelect(nums, 0, len(nums) - 1, len(nums) - k)  

    def quickSelect(self, nums, start, end, k):  
        pivot = nums[start]  
        left, right = self.partition(nums, start, end, pivot)  
        <u>**_if k <= right:_**</u>  
            return self.quickSelect(nums, start, right, k)  
        <u>_**elif k >= left:**_</u>  
            return self.quickSelect(nums, left, end, k)  
        <u>_**else:**_</u>  
            return nums[k]  

    # all the elements with idx < left are with values <= povot  
    # all the elements in the idx range []????  
    def partition(self, nums, left, right, pivot):  
        <u>_**while left <= right:**_</u>  
            <u>_**while nums[left] <**_</u><u>_ **pivot**_</u> and left <= right:  
                left+=1  
            <u>_**while nums[right] >**_</u><u>_ **pivot**_</u> and left <= right:  
                right-=1  
            <u>_**if left <= right**_</u>:  
                nums[left], nums[right] = nums[right], nums[left]  
                left+=1  
                right-=1  
        return left, right  
 </pre>

### **2.2 Tail to Head Iteration**

**Shuffle List - iterate from tail to head**  

<pre id="VCCACAbVZr1">def shuffle(nums):  
"""  
Returns a random shuffling of the array.  
:rtype: List[int]  
"""  
for i in <u>_**range**_</u><u>_**(len(nums) - 1, 0, -1**_</u><u>_**)**_</u>:  
    # swap arbitrary element before i (or i itself) and i  
    <u>_**j** _</u><u>_**= random.randrange(i + 1)**_</u>  
    nums[i], nums[j] = nums[j], nums[i]  
    # origin  = nums[j]  
    # nums[j] = nums[i]  
    # nums[i] = origin  
return nums</pre>

### **2.3 **Prefix-Sum****

**Subarray Sum Series**  
**Example: Subarray Sum Equals K (**Prefix sum + Dict)  

<pre id="VCCACAW1BlO">from collections import Counter  
class App(object):  
    def subarraySum(self, nums, k): # rtype: int  
        result = 0  
        prefix_sum = 0  
        prefix_sum_dict = Counter()  
        prefix_sum_dict[0] = 1 # 1 1, k = 2, should return 1  
        for i, num in enumerate(nums):  
            prefix_sum += num  
            result += (prefix_sum_dict[prefix_sum - k])  
            prefix_sum_dict[prefix_sum] += 1  
        return result</pre>

Reference: [https://leetcode.com/explore/interview/card/facebook/5/round-1-phone-interview/297/](https://leetcode.com/explore/interview/card/facebook/5/round-1-phone-interview/297/)  

Prefix sum must be for POSITIVE INTEGERS!!!!  

### **2.4 List &** Pointers****

One pointer: Stepping, Prefix-Sum (DP)  
Two pointer Race: Check Cycle (Slow/Fast)  
Two pointer Moving: Sliding Window, Quick Select (Swap)  
Two pointer Range: Binary Search  
List Manipulation: Two Element Swap / Flipping /Rotation (By Flipping/Swapping)  

<div data-section-style="13">

<table id="VCCACA6efl9" title="Sheet1" style="width: 43.2667em">

<thead>

<tr>

<th class="empty" style="width: 2em"></th>

<th id="VCCACAl83t6" class="empty" style="width: 12.2667em">A  
</th>

<th id="VCCACADnXNv" class="empty" style="width: 17.2em">B  
</th>

<th id="VCCACAjCX6Y" class="empty" style="width: 13.8em">C  
</th>

</tr>

</thead>

<tbody>

<tr id="VCCACAmORar">

<td style="background-color:#f0f0f0">1</td>

<td id="s:VCCACAmORar;VCCACAbuTwe" style="background-color:#a5a5a5;text-align: left;vertical-align: top;">  

</td>

<td id="s:VCCACAmORar;VCCACAe4hmC" style="background-color:#a5a5a5;text-align: left;vertical-align: top;">  
****General List****  
</td>

<td id="s:VCCACAmORar;VCCACAd3W0S" style="background-color:#a5a5a5;text-align: left;vertical-align: top;">  
****Sorted List****  
</td>

</tr>

<tr id="VCCACAEff2K">

<td style="background-color:#f0f0f0">2</td>

<td id="s:VCCACAEff2K;VCCACAbuTwe" style="background-color:#a5a5a5;text-align: left;vertical-align: top;">  
****Single Pointer** ******Stepping****  
</td>

<td id="s:VCCACAEff2K;VCCACAe4hmC" style="background-color:#dbdbdb;text-align: left;vertical-align: top;">  

</td>

<td id="s:VCCACAEff2K;VCCACAd3W0S" style="background-color:#dbdbdb;text-align: left;vertical-align: top;">  

</td>

</tr>

<tr id="VCCACA9LkFQ">

<td style="background-color:#f0f0f0">3</td>

<td id="s:VCCACA9LkFQ;VCCACAbuTwe" style="background-color:#a5a5a5;text-align: left;vertical-align: top;">  
****Single Pointer Stepping for** ******Preprocessing****  
</td>

<td id="s:VCCACA9LkFQ;VCCACAe4hmC" style="background-color:#ededed;text-align: left;vertical-align: top;">  
Prefix-sum  
</td>

<td id="s:VCCACA9LkFQ;VCCACAd3W0S" style="background-color:#ededed;text-align: left;vertical-align: top;">  

</td>

</tr>

<tr id="VCCACA2ul5c">

<td style="background-color:#f0f0f0">4</td>

<td id="s:VCCACA2ul5c;VCCACAbuTwe" style="background-color:#a5a5a5;text-align: left;vertical-align: top;">  
****Stepping for two sorted arrays - merging****  
</td>

<td id="s:VCCACA2ul5c;VCCACAe4hmC" style="background-color:#dbdbdb;text-align: left;vertical-align: top;">  

</td>

<td id="s:VCCACA2ul5c;VCCACAd3W0S" style="background-color:#dbdbdb;text-align: left;vertical-align: top;">  
Merging  
</td>

</tr>

<tr id="VCCACAnE6ow">

<td style="background-color:#f0f0f0">5</td>

<td id="s:VCCACAnE6ow;VCCACAbuTwe" style="background-color:#a5a5a5;text-align: left;vertical-align: top;">  
****Left Forward, Left Forward (2 Pointers Stepping)****  
</td>

<td id="s:VCCACAnE6ow;VCCACAe4hmC" style="background-color:#ededed;text-align: left;vertical-align: top;">  
Sliding Windows  
</td>

<td id="s:VCCACAnE6ow;VCCACAd3W0S" style="background-color:#ededed;text-align: left;vertical-align: top;">  
Find Duplication /  
Value Difference (a[i] – a[i-1])  
</td>

</tr>

<tr id="VCCACA6iBv4">

<td style="background-color:#f0f0f0">6</td>

<td id="s:VCCACA6iBv4;VCCACAbuTwe" style="background-color:#a5a5a5;text-align: left;vertical-align: top;">  
****Left Forward, Right Backward (2 Pointers Stepping) 前后指针+Swap****  
</td>

<td id="s:VCCACA6iBv4;VCCACAe4hmC" style="background-color:#dbdbdb;text-align: left;vertical-align: top;">  
Quick Select (Value → Rank) – O(n)  
Right is included in the range  
left左边是所有小于pivot的数字，right右边是所有大于pivot的数字  
pivot = A [(start + end) / 2]  
</td>

<td id="s:VCCACA6iBv4;VCCACAd3W0S" style="background-color:#dbdbdb;text-align: left;vertical-align: top;">  
Two Sums (Find two elements sum to n)  
</td>

</tr>

<tr id="VCCACASGRoz">

<td style="background-color:#f0f0f0">7</td>

<td id="s:VCCACASGRoz;VCCACAbuTwe" style="background-color:#a5a5a5;text-align: left;vertical-align: top;">  
****Range within start + end pointers 前后范围二分法****  
</td>

<td id="s:VCCACASGRoz;VCCACAe4hmC" style="background-color:#ededed;text-align: left;vertical-align: top;">  

</td>

<td id="s:VCCACASGRoz;VCCACAd3W0S" style="background-color:#ededed;text-align: left;vertical-align: top;">  
Binary Search  
</td>

</tr>

<tr id="VCCACAUTvFc">

<td style="background-color:#f0f0f0">8</td>

<td id="s:VCCACAUTvFc;VCCACAbuTwe" style="background-color:#a5a5a5;text-align: left;vertical-align: top;">  
****Fast Pointer + Slow Pointer****  
</td>

<td id="s:VCCACAUTvFc;VCCACAe4hmC" style="background-color:#dbdbdb;text-align: left;vertical-align: top;">  
Check Cycles  
</td>

<td id="s:VCCACAUTvFc;VCCACAd3W0S" style="background-color:#dbdbdb;text-align: left;vertical-align: top;">  

</td>

</tr>

<tr id="VCCACAQMz7m">

<td style="background-color:#f0f0f0">9</td>

<td id="s:VCCACAQMz7m;VCCACAbuTwe" style="background-color:#a5a5a5;text-align: left;vertical-align: top;">  
****Flipping********/Rotation****  
</td>

<td id="s:VCCACAQMz7m;VCCACAe4hmC" style="background-color:#ededed;text-align: left;vertical-align: top;">  

</td>

<td id="s:VCCACAQMz7m;VCCACAd3W0S" style="background-color:#ededed;text-align: left;vertical-align: top;">  
Rotate an array of n elements to the lift / to the right  
</td>

</tr>

</tbody>

</table>

</div>

**Example: Rotate Array**  
**Move Zeros (Use Pointers as a boundry)**  
Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.  

<pre id="VCCACAle0rz">def moveZeroes(nums):  
    i = 0  
    for j in range(len(nums)):  
        if nums[j]:  
            nums[i], nums[j] = nums[j], nums[i]  
            i += 1</pre>

**Minimum Window Substring (Use left + right pointers as a mini window)**  

<pre id="VCCACAvHrmv">class Solution:  
    def minWindow(self, s, t):  
        need, missing = collections.Counter(t), len(t)  
        **i** **= 0**  
       **I** **= 0**  
       **J** **= sys.maxsize**  
        **for j in range(len(s****))**: # the starting idx (j) is 1 to point to the first char  
            c = s[j]  
            missing -= need[c] > 0  
            need[c] -= 1  
            **if not missing:  # if condition is met**   
                # push left pointer while maintain the current condition  
                #-- left pointer is inclusive in the cur solution  
                while i <= j and **need****[s[i]] < 0:**   
                    # while i <= j is optional  
                    need[s[i]] += 1  
                    i += 1  
                **# update results**  
                if j - i <= J - I:  
                    I, J = i, j  
        **if J == sys.maxsize: return ""**  
        return s[I:J + 1]</pre>

Similar questions: [https://leetcode.com/explore/interview/card/facebook/5/round-1-phone-interview/328/](https://leetcode.com/explore/interview/card/facebook/5/round-1-phone-interview/328/)  

**Use Left, Right Pointers to Record the max value so far from left / right**  
# another option: use a list (some memory) to record the max right so far. (Space will not be O(1))  

**Example: Trapping Rain Water**  
Given _n_ non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining. The above elevation map is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.  

<pre id="VCCACAFovD8">**Input:** [0,1,0,2,1,0,1,3,2,1,2,1] **Output:** 6</pre>

<pre id="VCCACALtJgK">class Solution(object):  
    def trap(self, height):  
        n = len(height)  
        l, r, water, minHeight = 0, n - 1, 0, 0  
       **while l < r:**  
            **while l <** **r** and height[l] <= minHeight:  
                water += minHeight - height[l]  
                l += 1  
            while r > l and height[r] <= minHeight:  
                water += minHeight - height[r]  
                r -= 1  
            minHeight = min(height[l], height[r])  
        return water</pre>

### **2.5 List &** Stack****

Stack (1) 保存有效信息以便后续操作 (2)  翻转 (3) Monotonous stack 单调栈   
<u>_**Stack of values / indexes !**_</u>  

**Example: Implement Queue using Stacks** - O(1) amortized  

<pre id="VCCACAbJfU8"># Implement Queue using Stacks - O(1) amortized,  
# 翻转栈的运用  
class Queue(object):  
    def __init__(self):  
        """  
        initialize your data structure here.  
        """  
        self.inStack, self.outStack = [], []  

    def push(self, x):  
        """  
        :type x: int  
        :rtype: nothing  
        """  
        self.inStack.append(x)  

    def pop(self):  
        """  
        :rtype: nothing  
        """  
        self.move()  
        self.outStack.pop()  

    def peek(self):  
        """  
        :rtype: int  
        """  
        self.move()  
        return self.outStack[-1]  

    def empty(self):  
        """  
        :rtype: bool  
        """  
        return (not self.inStack) and (not self.outStack)   

    def move(self):  
        """  
        :rtype nothing  
        """  
        if not self.outStack:  
            while self.inStack:  
                self.outStack.append(self.inStack.pop())</pre>

<pre id="VCCACAL449T"># Related: Implement Stack using Queues - Push is O(n), others are O(1)  
class MyStack:  
    def __init__(self):  
        self._queue = collections.deque()  

    def push(self, x):  
        q = self._queue  
        q.append(x)  
        for _ in range(len(q) - 1):  
            q.append(q.popleft())  

    def pop(self):  
        return self._queue.popleft()  

    def top(self):  
        return self._queue[0]  

    def empty(self):  
        return not len(self._queue)  

# Related: Valid Parentheses  
# 保存有效信息以便后续操作  
class Solution:  
    def isValid(self, s):  
        """  
        :type s: str  
        :rtype: bool  
        Stack must be used here for the case   
        Input: "([)]"  
        Output: false  
        """  
        stack = []  
        chars = "()[]{}"  
        for c in s:  
            q = chars.index(c)  
            if q % 2 == 1: # use the idex of chars to indicate ()[]{}  
                if not stack or stack.pop() != q - 1:  
                    return False  
            else:  
                stack.append(q)  
        return len(stack) == 0  
</pre>

Stack: （1）保存有效信息以便后续操作 （2） 翻转  

Monotonous stack: 单调栈 — 找每一个元素左边或者右边，第一个比自身小/大的元素  

单调栈：递增栈是维护递增的顺序，当遇到小于栈顶元素的数就开始处理，而递减栈正好相反，维护递减的顺序，当遇到大于栈顶元素的数开始处理.  

**单调递增栈可以找到左起第一个比当前数字小的元素**。比如数组 [2 1 4 6 5]，刚开始2入栈，数字1入栈的时候，发现栈顶元素2比较大，将2移出栈，此时1入栈。那么2和1都没左起比自身小的数字。然后数字4入栈的时候，栈顶元素1小于4，于是1就是4左起第一个小的数字。此时栈里有1和4，然后数字6入栈的时候，栈顶元素4小于6，于是4就是6左起第一个小的数字。此时栈里有1，4，6，然后数字5入栈的时候，栈顶元素6大于5，将6移除，此时新的栈顶元素4小于5，那么4就是5左起的第一个小的数字，最终栈内数字为1，4，5。  

**单调递减栈可以找到左起第一个比当前数字大的元素**。See the example below。  
递减栈会剔除波谷，留下波峰；递增栈剔除波峰，留下波谷。  

明白了单调栈的加入元素的过程后，我们来看看它的性质，以及为啥要用单调栈。单调栈的一大优势就是线性的时间复杂度，所有的元素只会进栈一次，而且一旦出栈后就不会再进来了。  

**Example: (LC654) Maximum Binary Tree**  
Given an integer array with no duplicates. A max tree building on this array is defined as follow:  

<div data-section-style="5" style="" class="">

*   The root is the maximum number in the array  

*   The left subtree and right subtree are the max trees of the subarray divided by the root number.  

</div>

Construct the max tree by the given array.  

**Example**  
Given [2, 5, 6, 0, 3, 1], the max tree is  

<pre id="VCCACAPZb50">     6  
    / \  
   5   3  
  /   / \  
 2   0   1</pre>

[10, 2, 5, 3, 4, 6, 1]  

<pre id="VCCACAXo1PD">       10  
        \  
         6  
        / \  
       5   1  
      / \  
     2   4  
        /   
       3    </pre>

[3,2,1,6,0,5]  

<pre id="VCCACAJ7DDe">         6  
      /     \  
     3       5  
      \     /  
       2   0   
        \  
         1  

 </pre>

这种树叫做笛卡树（ Cartesian tree）。直接递归建树的话复杂度最差会退化到O(n^2)。  
自下而上也是经典建树方法，如2 5 6 0 3 1，2的parent肯定是比2大的元素。  
让后面element主动去当前面element的children，而不是前面element找后面element去找children  
For a element:   
  right child: In the view of the right child, its parent is **its 左起第一个比当前数字大的元素**  
  left child:   The max value below the current value, which is to the right of the last peak value greater than current value  
    E.g. [2, 5, 6, 0, <u>_**3**_</u>, 1] 3 should find 0 as left pointer because 0 is after 6.  

用到的是单调栈 (递减)。  
Monotonic Decreasing Stack:  
--- Monotic Decreasing Stack will keep<u>_ **the max element so far**_</u> and all the decreasing element right after it.  
  when 维护递减栈, the elements being pop are elements after last peak element below the current pushing element  
  when 加入  
[2, 5, 6, 0, 3, 1]  
2: [2]  
5: [5]  
6: [6]   
0: [6, 0]  
3: [6, 3]  
1: [6, 3, 1]  

因为题目中构建树的要求是：  
    对于每一个element，_<u>**找左边第一个比它小的 ()**</u>_，  
**_<u>找右边第一个比它小的 (右边递减单调栈入**_<u>栈时设前一个right pointer</u>_**)</u>_**，取最小。  
<u>_**递减栈可以找到向左走第一个比当前数字大的元素**_</u>  

<pre id="VCCACABE1sH">class Solution_simple_smart_iterative:  
    def constructMaximumBinaryTree(self, nums):  
        stack = []  
        for i in range(len(nums)):  
            cur = TreeNode(nums[i])  
            while stack and stack[-1].val < nums[i]: # 维护递减栈  
                cur.left = stack.pop()  
            if stack: # 递减栈可以找到向左走第一个比当前数字大的元素  
                stack[-1].right = cur  
            stack.append(cur)  
        return stack[0]</pre>

**Example. (LC84) Largest Rectangle in Histogram**  
Given _n_ non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.  

<div data-section-style="11" style="max-width:100%">![](https://quip.com/blob/VCCAAAgSiOv/DhN2wxeH_HqxbsE7AVBrUA?a=ANhtUAyYGalJVaWfGpku3C2ai9uyOfyoB9OA5opna0ga)</div>

Above is a histogram where width of each bar is 1, given height = `[2,1,5,6,2,3]`.  
The largest rectangle is shown in the shaded area, which has area = `10` unit.  

Note: 递增stack，因为需要all recent elements above the current element since the last min element.  
<u>_**Stack of indexes**_</u>  

<pre id="VCCACAVZAbR">**Input:** [2,1,5,6,2,3]  
**Output:** 10</pre>

<pre id="VCCACAynFnx">class Solution(object):  
    def largestRectangleArea(self, heights):  
        """  
        :type heights: List[int]  
        :rtype: int  
        """  
        stack = []  
        result = 0  
        _<u>**heights**</u>__<u>**.append(0)**</u>_  
        for i, height in enumerate(heights):  
            while stack and heights[stack[-1]] > height:  
                _<u>**idx** </u>__<u>**= stack.pop()**</u>_  
                last_idx = -1  
                _<u>**if stack:**</u>_  
                    last_idx = stack[-1]  
                result = max(result, (i - _<u>**last_idx**</u>_ - 1) * _<u>**heights**</u>__<u>**[idx**</u>__<u>**]**</u>_)  
            stack.append(i)  
        return result</pre>

**Example. (LC85) Maximal Rectangle**  
Given a 2D binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.  

**Example:**  

<pre id="VCCACAkame5">**Input:**  
[  
  ["1","0","1","0","0"],  
  ["1","0","**1**","**1**","**1**"],  
  ["1","1","**1**","**1**","**1**"],  
  ["1","0","0","1","0"]  
]  
**Output:** 6</pre>

<pre id="VCCACADbmK3">class Solution(object):  
    def maximalRectangle(self, matrix):  
        """  
        :type matrix: List[List[str]]  
        :rtype: int  
        """  
        if not matrix:  
            return 0  
        heights = [0] * len(matrix[0])  
        result = 0  
        for row in matrix:  
            for i, v in enumerate(row):  
                if v == '0':  
                    heights[i] = 0  
                if v == '1':  
                    heights[i] += 1  
            result = max(result, self.largestRectangleArea(heights))  
        return result  

    def largestRectangleArea(self, heights):  
        """  
        :type heights: List[int]  
        :rtype: int  
        """  
        stack = []  
        result = 0  
        heights.append(0)  
        for i, height in enumerate(heights):  
            # mono stack [smallest -> largest]  
            #   but storing index instead of (value, index)  
            while stack and heights[stack[-1]] > height:  
                idx = stack.pop()  
                last_idx = -1  
                if stack:  
                    last_idx = stack[-1]  
                result = max(result, (i - last_idx - 1) * heights[idx])  
            stack.append(i)  
        return result</pre>

**Related: Maximal Square**  

<pre id="VCCACAlkF3S">class Solution:  
    def maximalSquare(self, matrix):  
        """  
        :type matrix: List[List[str]]  
        :rtype: int  

        matrix:  
        1 0 1 0 0  
        1 0 1 1 1  
        1 1 1 1 1  
        1 0 0 1 0  
        m = 4, n = 5  

        maximal_square_size:  
        1 0 1 0 0  
        1 0 2 2 1  
        1 1 1 1 1  
        1 0 0 1 0  
        """  
        m = len(matrix)  
        if not m: return 0  
        n = len(matrix[0])  
        if not n: return 0  
        maximal_square_size = [[int(matrix[i][j]) for j in range(n)] for i in range(m)]  
        result = 0  
        for i in range(m - 1, -1, -1):  
            for j in range(n - 1, -1, -1):  
                if not (i == m - 1 or j == n - 1) and maximal_square_size[i][j] == 1:  
                    maximal_square_size[i][j] = min(maximal_square_size[i + 1][j],   
                                                    maximal_square_size[i][j + 1],  
                                                    maximal_square_size[i + 1][j + 1]) + 1  
                result = max(result, maximal_square_size[i][j])  
        return result ** 2</pre>

### **2.6 List &** Deque****

**Example: Shortest Subarray with Sum at Least K**  
Return the length of the shortest, non-empty, contiguous subarray of A with sum at least K.  
If there is no non-empty subarray with sum at least K, return -1.  
Example 1: Input: A = [1], K = 1 Output: 1  
Example 2: Input: A = [1,2], K = 4 Output: -1  
Example 3: Input: A = [2,-1,2], K = 3 Output: 3  

<pre id="VCCACA38PQ6">from collections import deque  
class Solution(object):  
    def shortestSubarray(self, A, K):  
        """  
        :type A: List[int]  
        :type K: int  
        :rtype: int  

        所以要换个思路，对于每个以i结尾的子数组，有效的开头可能有很多；  
        暴力的方法就是遍历每个有效的开头求最小的length，  
        但是这些有效的开头都是有重叠的，  
        一个优化的思路就是能不能每次不遍历所有有效开头，维护一个数据结构，  
        每次都更新这个数据结构的value，从而避免重复运算  

        https://www.gjxhlan.me/2018/07/07/leetcode-contest-91-solution/  
        """  
        # 如若有比K大的数，则直接返回1  
        if max(A) >= K: return 1  

        # 记录和，dp[i] = sum(A[:i])  
        dp = [0] * (len(A)+1)  
        for i in range(1,len(dp)):  
            dp[i] = dp[i-1] + A[i-1]  

        res = float('inf')  
        # 初始化队列  
        Q = deque([0]) # a deque containing all indexes  
        # 1 2 -10 3 5 3 9,  k = 4  
        for i in range(1,len(dp)):  
            # 思路中第2步  
            while Q and dp[i]-dp[Q[0]] >= K:  
                res = min(res,i-Q.popleft())  
            # 思路中第3步  
            while Q and  dp[i]<dp[Q[-1]]: # similar to the idea of monotonic stack  
                Q.pop()  
            Q.append(i)   
        return [res,-1][res==float('inf')]</pre>

### **2.7 ****Flipping ********/ Rotation******

**Example: Rotate Array**  

<pre id="VCCACAuHSLa"># Rotate by Reversion  
public class Solution {  
    public void rotate(int[] nums, int k) {  
        k %= nums.length;  
        reverse(nums, 0, nums.length - 1);  
        reverse(nums, 0, k - 1);  
        reverse(nums, k, nums.length - 1);  
    }  
    public void reverse(int[] nums, int start, int end) {  
        while (start < end) {  
            int temp = nums[start];  
            nums[start] = nums[end];  
            nums[end] = temp;  
            start++;  
            end--;  
        }  
    }  
}  

# Rotate Only By One  
#Function to left rotate arr[] of size n by d*/  
def leftRotate(arr, d, n):  
    for i in range(d):  
        leftRotatebyOne(arr, n)  

#Function to left Rotate arr[] of size n by 1*/   
def leftRotatebyOne(arr, n):  
    temp = arr[0]  
    for i in range(n-1):  
        arr[i] = arr[i+1]  
    arr[n-1] = temp</pre>

### **2.8 _Continuous Nums_**

_Modify array itself as a hash map to make space complexity to be O(1)._  

**Example:**  First Missing Positive  
First Missing Positive: Given an unsorted integer array, find the smallest missing positive integer.  
Example 1: Input: [1,2,0] Output: 3  
Example 2: Input: [3,4,-1,1] Output: 2  
Example 3: Input: [7,8,9,11,12] Output: 1  
Note: Your algorithm should run in O(n) time and uses constant extra space.  

虽然不能再另外开辟非常数级的额外空间，但是可以在输入数组上就地进行swap操作。  
**思路**：交换数组元素，使得数组中第i位存放数值(i+1)。最后遍历数组，寻找第一个不符合此要求的元素，返回其下标。整个过程需要遍历两次数组，复杂度为_O(n)_。---> By Swap One Time, An element will be settled to the correct place.   

<div data-section-style="11" style="max-width:100%">![](https://quip.com/blob/VCCAAAgSiOv/YhjK0vNqoh7IpTxdw_MYbg?a=uUqfpJRH7AnZmLvhMG3Qvzh9bzvR7qkz16gDANu6XZka)</div>

<pre id="VCCACA4fnB6">class Solution {  
public:  
    int firstMissingPositive(int A[], int n) {  
        int i = 0;  
        while (i < n) {  
            if (A[i] != (i+1) && A[i] >= 1 &&  
                 A[i] <= n <u>_**&& A[A[i]-1] != A[i**_</u><u>_**]**_</u>)  
                swap(A[i], A[A[i]-1]);  
            else  
                i++;  
        }  
        for (i = 0; i < n; ++i)  
            if (A[i] != (i+1))  
                return i+1;  
        return n+1;  
    }  
};</pre>

### **2.9 List & Map & Set**

<div data-section-style="13">

<table id="VCCACAWTaZV" title="Sheet2" style="width: 51.8em">

<thead>

<tr>

<th class="empty" style="width: 2em"></th>

<th id="VCCACAUUUH2" class="empty" style="width: 21.7333em">A  
</th>

<th id="VCCACAjqXrb" class="empty" style="width: 6em">B  
</th>

<th id="VCCACATJNEW" class="empty" style="width: 24.0667em">C  
</th>

</tr>

</thead>

<tbody>

<tr id="VCCACAqhcm5">

<td style="background-color:#f0f0f0">1</td>

<td id="s:VCCACAqhcm5;VCCACAbehfK" style="background-color:#eeddee;vertical-align: middle;">  
**Operation**  
</td>

<td id="s:VCCACAqhcm5;VCCACAQgNTW" style="background-color:#eeddee;vertical-align: middle;">  
**Equivalent**  
</td>

<td id="s:VCCACAqhcm5;VCCACAw6J9r" style="background-color:#eeddee;vertical-align: middle;">  
**Result**  
</td>

</tr>

<tr id="VCCACAMIu1a">

<td style="background-color:#f0f0f0">2</td>

<td id="s:VCCACAMIu1a;VCCACAbehfK" style="background-color:#eeeeff;vertical-align: middle;">  
`s.pop()`  
</td>

<td id="s:VCCACAMIu1a;VCCACAQgNTW" style="background-color:#eeeeff;vertical-align: middle;">  

</td>

<td id="s:VCCACAMIu1a;VCCACAw6J9r" style="background-color:#eeeeff;vertical-align: middle;">  
Pop a random element from s  
</td>

</tr>

<tr id="VCCACAwxlS8">

<td style="background-color:#f0f0f0">3</td>

<td id="s:VCCACAwxlS8;VCCACAbehfK" style="background-color:#eeeeff;vertical-align: middle;">  
`x in s`  
</td>

<td id="s:VCCACAwxlS8;VCCACAQgNTW" style="background-color:#eeeeff;vertical-align: middle;">  

</td>

<td id="s:VCCACAwxlS8;VCCACAw6J9r" style="background-color:#eeeeff;vertical-align: middle;">  
test _x_ for membership in _s_  
</td>

</tr>

<tr id="VCCACAwTOjH">

<td style="background-color:#f0f0f0">4</td>

<td id="s:VCCACAwTOjH;VCCACAbehfK" style="background-color:#eeeeff;vertical-align: middle;">  
`x not in s`  
</td>

<td id="s:VCCACAwTOjH;VCCACAQgNTW" style="background-color:#eeeeff;vertical-align: middle;">  

</td>

<td id="s:VCCACAwTOjH;VCCACAw6J9r" style="background-color:#eeeeff;vertical-align: middle;">  
test _x_ for non-membership in _s_  
</td>

</tr>

<tr id="VCCACAesd9a">

<td style="background-color:#f0f0f0">5</td>

<td id="s:VCCACAesd9a;VCCACAbehfK" style="background-color:#eeeeff;vertical-align: middle;">  
`s.issubset(t)`  
</td>

<td id="s:VCCACAesd9a;VCCACAQgNTW" style="background-color:#eeeeff;vertical-align: middle;">  
`s <= t`  
</td>

<td id="s:VCCACAesd9a;VCCACAw6J9r" style="background-color:#eeeeff;vertical-align: middle;">  
test whether every element in _s_ is in _t_  
</td>

</tr>

<tr id="VCCACAkSkqw">

<td style="background-color:#f0f0f0">6</td>

<td id="s:VCCACAkSkqw;VCCACAbehfK" style="background-color:#eeeeff;vertical-align: middle;">  
`s.issuperset(t)`  
</td>

<td id="s:VCCACAkSkqw;VCCACAQgNTW" style="background-color:#eeeeff;vertical-align: middle;">  
`s >= t`  
</td>

<td id="s:VCCACAkSkqw;VCCACAw6J9r" style="background-color:#eeeeff;vertical-align: middle;">  
test whether every element in _t_ is in _s_  
</td>

</tr>

<tr id="VCCACAALXUt">

<td style="background-color:#f0f0f0">7</td>

<td id="s:VCCACAALXUt;VCCACAbehfK" style="background-color:#eeeeff;vertical-align: middle;">  
`**s.union(t)**`  
</td>

<td id="s:VCCACAALXUt;VCCACAQgNTW" style="background-color:#eeeeff;vertical-align: middle;">  
`**s | t**`  
</td>

<td id="s:VCCACAALXUt;VCCACAw6J9r" style="background-color:#eeeeff;vertical-align: middle;">  
**new set with elements from both _s_ and _t_**  
</td>

</tr>

<tr id="VCCACAO5v7t">

<td style="background-color:#f0f0f0">8</td>

<td id="s:VCCACAO5v7t;VCCACAbehfK" style="background-color:#eeeeff;vertical-align: middle;">  
`**s.intersection(t)**`  
</td>

<td id="s:VCCACAO5v7t;VCCACAQgNTW" style="background-color:#eeeeff;vertical-align: middle;">  
`**s & t**`  
</td>

<td id="s:VCCACAO5v7t;VCCACAw6J9r" style="background-color:#eeeeff;vertical-align: middle;">  
**new set with elements common to _s_ and _t_**  
</td>

</tr>

<tr id="VCCACAyFxtz">

<td style="background-color:#f0f0f0">9</td>

<td id="s:VCCACAyFxtz;VCCACAbehfK" style="background-color:#eeeeff;vertical-align: middle;">  
`**s.difference(t)**`  
</td>

<td id="s:VCCACAyFxtz;VCCACAQgNTW" style="background-color:#eeeeff;vertical-align: middle;">  
`**s - t**`  
</td>

<td id="s:VCCACAyFxtz;VCCACAw6J9r" style="background-color:#eeeeff;vertical-align: middle;">  
**new set with elements in _s_ but not in _t_**  
</td>

</tr>

<tr id="VCCACAilzlL">

<td style="background-color:#f0f0f0">10</td>

<td id="s:VCCACAilzlL;VCCACAbehfK" style="background-color:#eeeeff;vertical-align: middle;">  
`**s.symmetric_difference(t)**`  
</td>

<td id="s:VCCACAilzlL;VCCACAQgNTW" style="background-color:#eeeeff;vertical-align: middle;">  
`**s ^ t**`  
</td>

<td id="s:VCCACAilzlL;VCCACAw6J9r" style="background-color:#eeeeff;vertical-align: middle;">  
**new set with elements in either _s_ or _t_ but not both**  
</td>

</tr>

</tbody>

</table>

</div>

## Topic 3: Linked List

### 3.1 Get Median / Reverse

Fast Pointer, Slow Pointer ---> Find median/ Tortoise and hare if there is an intersection;  
Pay attention to the case when a pointer is None;  
Pay attention to see if the linked list length is even or odd;  

**Example: Reorder List**  
Given a singly linked list _L_: _L_0→_L_1→…→_L__n_-1→_L_n,  
reorder it to: _L_0→_L__n_→_L_1→_L__n_-1→_L_2→_L__n_-2→…  
You may **not** modify the values in the list's nodes, only nodes itself may be changed.  

<pre id="VCCACAxwJRj">class Solution(object):  
    """  
    1->2->3->4->5, reorder it to 1->5->2->4->3.  
    1->2->3<-4<-5    
    1->2->3->4, reorder it to 1->4->2->3.  
    1->2->3<-4  
    """  
    def reorderList(self, head):  
        """  
        :type head: ListNode  
        :rtype: void Do not return anything, modify head in-place instead.  
        """  
        # Find the median (or next near median split) of the linked list:  
        head_fast = head  
        head_slow = head  
        while head_fast and head_fast.next:   
            # 1 -> 2 -> 3       head_fast will be 3 while head_slow is 2  
            # 1 -> 2 -> 3 -> 4  head_fast will be None while head_slow is 3  
            head_fast = head_fast.next.next  
            head_slow = head_slow.next  

        # Reverse linked list since head_slow:  
        #  1 -> 2 -> 3 -> 4    1 -> 2    4 -> 3  
        cur = None  
        cur_next = head_slow  
        while cur_next:  
            cur_next_next = cur_next.next  
            cur_next.next = cur  
            cur      = cur_next   
            cur_next = cur_next_next  

        l1 = head  
        l2 = cur  
        # Merge head and cur  
        while l1:  
            next_l1 = l1.next  
            l1.next = l2  
            if not l2: break  
            next_l2 = l2.next  
            l2.next = next_l1  
            l1      = next_l1  
            l2      = next_l2</pre>

**Example: Palindrome Linked List**  
Given a singly linked list, determine if it is a palindrome.  

<pre id="VCCACAMWTpM">**Input:** 1->2  
**Output:** false</pre>

<pre id="VCCACAyh8Mg">**Input:** 1->2->2->1  
**Output:** true</pre>

<pre id="VCCACAfHG4W">/**  
 * @param {ListNode} head  
 * @return {boolean}  
 1  
 1->1  
 1->2  
 1->4->3  
 1->4->1  
 */  
var isPalindrome = function(head) {  
    // know mid  
    // reverse before mid  
    // run backward and forward in pararrel since mid  
    let fast = head  
    let slow = head  
    let slowPrev = null  
    while (fast != null && fast.next != null) {   
        // 1->2->3 fast == 3 slow == 2 slowPrev == 1.  
        // 1->2->3->4 fast == null slowPrev == 2, slow == 3  
        fast = fast.next.next  
        let actualSlowNext = slow.next  
        slow.next = slowPrev  
        slowPrev = slow  
        slow = actualSlowNext  
    }  

    if (fast != null) { // if odd, move slow one step forward  
        slow = slow.next  
    }  

    while (slow != null) {  
        if (slow.val != slowPrev.val) {  
            return false  
        }  
        slow = slow.next  
        slowPrev = slowPrev.next  
    }  

    return true  
};</pre>

### 3.2 Utilize Helpers

**Example: Convert Binary Search Tree to Sorted Doubly Linked List**  
Convert a BST to a sorted circular doubly-linked list in-place. Think of the left and right pointers as synonymous to the previous and next pointers in a doubly-linked list.  
Let's take the following BST as an example, it may help you understand the problem better:  

We want to transform this BST into a circular doubly linked list. Each node in a doubly linked list has a predecessor and successor. For a circular doubly linked list, the predecessor of the first element is the last element, and the successor of the last element is the first element.  
The figure below shows the circular doubly linked list for the BST above. The "head" symbol means the node it points to is the smallest element of the linked list.  

Specifically, we want to do the transformation in place. After the transformation, the left pointer of the tree node should point to its predecessor, and the right pointer should point to its successor. We should return the pointer to the first element of the linked list.  
The figure below shows the transformed BST. The solid line indicates the successor relationship, while the dashed line means the predecessor relationship.  

<div data-section-style="11" style="max-width:100%">![](https://quip.com/blob/VCCAAAgSiOv/tV1cxTxpzqK54zPMppFlfQ?a=qj4v6sR5B6uEatdCZbmSgRqDAIigkEa6hKudOady3FUa)</div>

<div data-section-style="11" style="max-width:100%">![](https://quip.com/blob/VCCAAAgSiOv/RbRCgFk7268odqJYapQi5g?a=Uat2ABhrXVpoA6fXZ2SDPadrgd4D6F2ggjUFp3GYzJYa)</div>

<div data-section-style="11" style="max-width:100%">![](https://quip.com/blob/VCCAAAgSiOv/srqGoZkD86qvbvuRH7hmkQ?a=YOdCya7Eralv62TnBXrMGliua4bqI7csOazScEdp128a)</div>

<pre id="VCCACAp3p9L">class Solution {  
    public Node treeToDoublyList(Node root) {  
        if (root == null) {  
            return null;  
        }  

        Node leftHead = treeToDoublyList(root.left);  
        Node rightHead = treeToDoublyList(root.right);  
        root.left = root;  
        root.right = root;  
        return connect(connect(leftHead, root), rightHead);  
    }  

    // Used to connect two circular doubly linked lists.   
    // n1 is the head as well as n2.  
    private Node connect(Node n1, Node n2) {  
        if (n1 == null) {  
            return n2;  
        }  

        if (n2 == null) {  
            return n1;  
        }  

        Node tail1 = n1.left;  
        Node tail2 = n2.left;  

        tail1.right = n2;  
        n2.left = tail1;  
        tail2.right = n1;  
        n1.left = tail2;  

        return n1;  
    }  
}</pre>

**Example: Merge k Sorted Linked List**  
Merge _k_ sorted linked lists and return it as one sorted list. Analyze and describe its complexity.  
Time complexity: O(n*logk)  

<pre id="VCCACA3XvIV"># Definition for singly-linked list.  
# class ListNode:  
#     def __init__(self, x):  
#         self.val = x  
#         self.next = None  

class Solution:  
    def conquer(self, a, b):  
        head = cur = ListNode(None) # Dummy Node  
        while a and b:  
            if a.val < b.val:  
                cur.next = a  
                a = a.next  
            else:  
                cur.next = b  
                b = b.next  

            cur = cur.next  
            cur.next = None  
        if a:  
            cur.next = a  
        if b:  
            cur.next = b  
        return head.next  

    def conquer2(self, a, b):  
        head = ListNode(None) # Dummy Node  
        head.next = a  

        node = head  
        while node.next:  
            if b and node.next.val > b.val:  
                pre_next  = node.next  
                node.next = b  
                b_next    = b.next  
                b.next    = pre_next  

                node      = b  
                b         = b_next  
            else:  
                node      = node.next  
        node.next = b  
        return head.next  

    def divide(self, lists, start, end):  
        """  
        *Input: *[ 1->4->5, 1->3->4, 2->6 ]  
*        Output:* 1->1->2->3->4->4->5->6  
        """  
        if start > end: return []  
        if start == end:  
            return lists[start]  
        mid   = (start + end) // 2  
        left  = self.divide(lists, start,   mid)  
        right = self.divide(lists, mid + 1, end)  
        return self.conquer(left, right)  

    def mergeKLists(self, lists):  
        """  
        :type lists: List[ListNode]  
        :rtype: ListNode  
        O R T  
        """  
        return self.divide(lists, 0, len(lists) - 1)</pre>

**Example: Populating Next Right Pointers in Each Node II**  
Given a binary tree  

<pre id="VCCACAtCIir">struct TreeLinkNode {  
  TreeLinkNode *left;  
  TreeLinkNode *right;  
  TreeLinkNode *next;  
}</pre>

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.  
Initially, all next pointers are set to `NULL`.  
**Note:**  

<div data-section-style="5" style="" class="">

*   You may only use constant extra space.  

*   Recursive approach is fine, implicit stack space does not count as extra space for this problem.  

</div>

**Example:**  
Given the following binary tree,  

<pre id="VCCACActorv">     1  
   /  \  
  2    3  
 / \    \  
4   5    7</pre>

After calling your function, the tree should look like:  

<pre id="VCCACAKHFNW">     1 -> NULL  
   /  \  
  2 -> 3 -> NULL  
 / \    \  
4-> 5 -> 7 -> NULL</pre>

<pre id="VCCACAjTFtX">class Solution:  
    # @param root, a tree link node  
    # @return nothing  
    def connect(self, head, next_pointer = None):  
        if not head:  
            return  
        head.next = next_pointer  
        new_next_pointer = self.find_next_pointer(head.next)  
        if head.right:  
            self.connect(head.right, new_next_pointer) # tail recursion optimization  
            self.connect(head.left, head.right)  
            # https://www.zhihu.com/question/20761771  
        else:  
            self.connect(head.left, new_next_pointer)  

    def find_next_pointer(self, next_node): # 3  
        while next_node: # 3  
            if next_node.left: return next_node.left  
            if next_node.right: return next_node.right  
            next_node = next_node.next  
        return None</pre>

**Example: Copy List with Random Pointer**  
A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null. Return a deep copy of the list.  

<pre id="VCCACASQfIk">class Solution(object):  
    def copyRandomList(self, head):  

        # Insert each node's copy right after it, already copy .label  
        node = head  
        while node:  
            copy = RandomListNode(node.label)  
            copy.next = node.next  
            node.next = copy  
            node = copy.next  

        # Set each copy's .random  
        node = head  
        while node:  
            node.next.random = node.random and node.random.next  
            node = node.next.next  

        # Separate the copied list from the original, (re)setting every .next  
        node = head  
        copy = head_copy = head and head.next  
        while node:  
            node.next = node = copy.next  
            copy.next = copy = node and node.next  

        return head_copy</pre>

### 3.3 COnnecting lists

One List can be rearrange to two; Two lists can be combined to one; Use Dummy Node here.  

**Example: Partition List**  
Given a linked list and a value _x_, partition it such that all nodes less than _x_ come before nodes greater than or equal to _x_.  
You should preserve the original relative order of the nodes in each of the two partitions.  
**  
Input:** head = 1->4->3->2->5->2, _x_ = 3  
**Output:** 1->2->2->4->3->5  

<pre id="VCCACAfE1bD"># Definition for singly-linked list.  
# class ListNode(object):  
#     def __init__(self, x):  
#         self.val = x  
#         self.next = None  

class Solution(object):  
    def partition(self, head, x):  
        """  
        :type head: ListNode  
        :type x: int  
        :rtype: ListNode  

        1->4->3->2->5->2, x = 3  
        1->4->3->2->5->2, x = 1  
        1->4->3->2->5->2, x = 5  
        1->4->3->2->5->2, x = 6  
        """  
        left  = left_head  = ListNode(None)  
        right = right_head = ListNode(None)  
        cur = head  
        while cur:  
            cur_next = cur.next  
            cur.next = None  
            if cur.val < x:  
                left.next = cur  
                left = cur  
            else:  
                right.next = cur  
                right = cur  
            cur = cur_next  
        left.next = right_head.next  
        return left_head.next  

    def partitionWithoutDummy(self, head, x):  
        """  
        :type head: ListNode  
        :type x: int  
        :rtype: ListNode  

        1->4->3->2->5->2, x = 3  
        1->4->3->2->5->2, x = 1  
        1->4->3->2->5->2, x = 5  
        1->4->3->2->5->2, x = 6  
        """  
        left  = left_head  = None  
        right = right_head = None  
        cur = head  
        while cur:  
            cur_next = cur.next  
            cur.next = None  
            if cur.val < x:  
                if not left:  
                    left = cur  
                    left_head = cur  
                else:  
                    left.next = cur  
                    left = cur  
            else:  
                if not right:  
                    right = cur  
                    right_head = cur  
                else:  
                    right.next = cur  
                    right = cur  
            cur = cur_next  
        if left:  
            left.next = right_head  
            return left_head  
        else:  
            return right_head</pre>

**Example: Reverse Linked List II**  
Reverse a linked list from position _m_ to _n_. Do it in one-pass.  
**Note:** 1 ≤ _m_ ≤ _n_ ≤ length of list.  
**Example:**  

<pre id="VCCACAqzFbD">**Input:** 1->2->3->4->5->NULL, _m_ = 2, _n_ = 4  
**Output:** 1->4->3->2->5->NULL</pre>

<pre id="VCCACABzApn">    def reverseBetween(self, head, m, n):  
        if m == n:  
            return head  

        dummyNode = ListNode(0)  
        dummyNode.next = head  
        pre = dummyNode  

        for i in range(m - 1):  
            pre = pre.next  

        # reverse the [m, n] nodes  
        reverse = None  
        cur = pre.next  
        for i in range(n - m + 1):  
            next = cur.next  
            cur.next = reverse  
            reverse = cur  
            cur = next  

        pre.next.next = cur  
        pre.next = reverse  

        return dummyNode.next</pre>

<pre id="VCCACAbsZ0g">class SolutionWithoutDummy(object):  
    def reverseBetween(self, head, m, n):  
        """  
        :type head: ListNode  
        :type m: int  
        :type n: int  
        :rtype: ListNode  

        [1,2,3,4,5]  
        2  
        4  
        """  
        if not head: return head  
        cur  = head  
        prev = None  
        n = n - m  
        while m > 1:  
            prev =  cur  
            cur  =  cur.next  
            m    -= 1  
        if cur:  
            reversed_sec, rest_sec = self.reverse_list(cur, n)  
            cur.next = rest_sec  
            if prev:  
                prev.next = reversed_sec  
            else: # if prev is None, then return the new head  
                return reversed_sec  
        return head  

    def reverse_list(self, head, k):  
        # input:  1->2->3->4->5->NULL, 2  
        # output: 3->2->1->NULL, 4->5->NULL  
        prev = None  
        cur  = head  

        while cur:  
            if k >= 0:  
                cur_next = cur.next  
                cur.next = prev  
                prev = cur  
                cur  = cur_next  
                k -= 1  
            else:  
                break  
        return (prev, cur)</pre>

### 3.4 Divide & Conquer

T(n) = T(n/2) + O(1) = O(logn),  
T(n) = T(n/2) + O(n) = O(n),  
T(n) = <u>_**2T(n/2) + O(1) = = 2T(n/2) + c = O(n)**_</u>,  example ==> n = 4  
T(n) =<u>_ **2T(n/2) + O(n) = O(n*logn)**_</u> example n = 4 ==> 4log4  
The last divide & conquer can generate a n*logn  

**Example: Merge k Sorted Array List**  
Merge _k_ sorted array lists and return it as one sorted list. Analyze and describe its complexity.  
Time complexity: O(n*logk)  

<pre id="VCCACAnSIij">**Input: **[ 1->4->5, 1->3->4, 2->6 ]  
**Output:** 1->1->2->3->4->4->5->6</pre>

<pre id="VCCACARlbz8"># Array List Based  
class Solution:  
    def two_list_merge(self, a, b):  
        # a = [], b = [1]  
        # a = [1, 3], b = [2, 4]  
        i, j = 0, 0  
        result = []  
        while i < len(a) and j < len(b):  
            if a[i] < b[j]:  
                result.append(a[i])  
                i += 1  
            else:  
                result.append(b[j])  
                j += 1  
        if i < len(a):  
            result += a[i:]  
        if j < len(b):  
            result += b[j:]  
        return result  

    def merge(self, lists, start, end):  
        """  
        *Input: *[ 1->4->5, 1->3->4, 2->6 ]  
*        Output:* 1->1->2->3->4->4->5->6  
        """  
        if start > end: return []  
        if start == end:  
            return lists[start]  
        mid   = (start + end) // 2  
        left  = self.merge(lists, start,   mid)  
        right = self.merge(lists, mid + 1, end)  
        return self.two_list_merge(left, right)  

    def mergeKLists(self, lists):  
        """  
        :type lists: List[ListNode]  
        :rtype: ListNode  
        O R T  
        """  
        return self.merge(lists, 0, len(lists) - 1)  
s = Solution()  
print(s.mergeKLists([[1,4,5],[1,3,4],[2,6]]))</pre>

## Topic 4: **String & List**

### 4.1 KMP - String Match

**Example: Implement strStr()  --- KMP algorithm**  
Return the index of the first occurrence of pattern in text, or -1 if pattern is not part of text.   
Next Table:  

<div data-section-style="11" style="max-width:100%">![](https://quip.com/blob/VCCAAAgSiOv/EUdROxsm5SK0sAYil8l5UA?a=vbMXJtsnohoLG1l0FjNLUARQXfyvUCb1JQR0fQyhZAca)</div>

<div data-section-style="11" style="max-width:100%">![](https://quip.com/blob/VCCAAAgSiOv/rnB2NzoEadzDYtZrOImRpA?a=7vdm9YfMcNO2J4NXZTeuAVZDZHa7xojCt72krQlsHKga)</div>

<div data-section-style="11" style="max-width:100%">![](https://quip.com/blob/VCCAAAgSiOv/Kl9PNmSLBLsfXk0oyqEszQ?a=U5VJoQualaOL4UKGnjUmbqe5gFil5LlLayDVnQ9vVwwa)</div>

移动位数 = 已匹配的字符数 - 对应的部分匹配值  
"部分匹配值"就是"前缀"和"后缀"的最长的共有元素的长度  
以"ABCDABD"为例  
－ "A"的前缀和后缀都为空集，共有元素的长度为0；  
－ "AB"的前缀为[A]，后缀为[B]，共有元素的长度为0；  
－ "ABC"的前缀为[A, AB]，后缀为[BC, C]，共有元素的长度0；  
－ "ABCD"的前缀为[A, AB, ABC]，后缀为[BCD, CD, D]，共有元素的长度为0；  
－ "ABCDA"的前缀为[A, AB, ABC, ABCD]，后缀为[BCDA, CDA, DA, A]，共有元素为"A"，长度为1；  
－ "ABCDAB"的前缀为[A, AB, ABC, ABCD, ABCDA]，后缀为[BCDAB, CDAB, DAB, AB, B]，共有元素为"AB"，长度为2；  
－ "ABCDABD"的前缀为[A, AB, ABC, ABCD, ABCDA, ABCDAB]，后缀为[BCDABD, CDABD, DABD, ABD, BD, D]，共有元素的长度为0。  

0是指下一个要去比较的是patter[0], 1是指下一个要去比较的是patter[1]  

<pre id="VCCACAKwUn6">def compute_prefix_function(pattern):  
    next_table = [0] * len(pattern)  
    k = 0 # k is the next char to compare in pattern  
    for q in range(1, len(pattern)):  
        while k > 0 and pattern[k] != pattern[q]:  
            k = next_table[k - 1]  
        if pattern[k] == pattern[q]:  
            k = k + 1  
        next_table[q] = k  
    return next_table  

def kmp_match(text, pattern):  
    next_table = compute_prefix_function(pattern)  
    q = 0 # q is the next char to compare in pattern  
    for i in range(len(text)):  
        while q > 0 and pattern[q] != text[i]:  
            q = next_table[q - 1]  
        if pattern[q] == text[i]:  
            q = q + 1  
        if q == len(pattern):  
            return i - len(pattern) + 1  
            # return the start idx of the matched pattern  
    return -1 # not found  

text    = 'BBC ABCDAB ABCDABCDABDE'  
pattern = 'ABCDABD'  
print(compute_prefix_function(pattern))  
# [0, 0, 0, 0, 1, 2, 0]  
print(kmp_match(text, pattern))   
# Expect to be idx 15</pre>

## Topic 5: **HashMap**

****Want to have all O(1)? – How to implement HashMap?  
A Hash Table dictionary contains: an array A with size M, key-value pairs, hash function  
Operations: search(k)** **– **insert (k, v), search (k)** return value of k / not exist**, update (k, v), delete(k)**  

Key Concerns:  
  (1) <u>_**Hash function**_</u> - what if keys are not integers?  
  (2)<u>_ **Good Hashing**_</u> - it maps the keys in our map so as to sufficiently minimize collisions  
        <u>_**Collection Handling**_</u>: If collection happens - how to handle collection? (Chaining or Open-Hashing)  
  (3) When and how to <u>_**extend the array when there are too many collisions** _</u>(too many numbers)?  

****Concern1: Hash Functions = Hash code function + Compression function****  
arrayIdx to place = hashcode % module len(capacity of array) - 1  

****Concern2: Chaining (bucketing) or Open-addressing****  

Chaining: Store the item (k,v) in the bucket A[h(k)].  
Open-addressing: If we try to insert an item (k,v) into a bucket A[j] that is already occupied, where j = h(k), then  
    we next try A[(j+1) mod N]. If A[(j+1) mod N] is also occupied, then we try A[( j+2) mod N], and so on,  
    until we find an empty bucket that can accept the new item.   
<u>In open-addressing, to implement a deletion, we cannot simply remove a found item</u> from its slot in the array. For example, after the insertion of key 15, if the item with key 37 were trivially deleted, a subsequent search for 15 would fail because that search would start by probing at index 4, then index 5, and then index 6, at which an empty cell is found. <u>A typical way to get around this difficulty is to replace a deleted item with a special</u> <u>“</u><u>available</u><u>”</u> <u>marker object.</u>  

<u>Open-addressing is usually faster than chained hashing when the load factor is low</u> because you don't have to follow pointers between list nodes. <u>It gets very, very slow if the load factor approaches 1,</u> because you end up usually having to search through many of the slots in the bucket array before you find either the key that you were looking for or an empty slot. Also, <u>you can never have more elements in the hash table than there are entries in the bucket array.</u>  

****Concern2: Load Factor (Extend the array & Rehashing)****  
In the hash table schemes described thus far, it is important that the load factor, L= n/N, be kept below 1,  
                                                                                         n == current hashtable length, N == hashtable capacity  
                                                                                       Since we want to have expected collection to be 1  
In Java, Default initial capacity of the HashMap takes is 16 and load factor is 0.75f (i.e 75% of current map size).  
In Python load factor is 0.5, If the load factor of the table increases beyond 0.5, we double the size of the table and rehash all items into the new table.  

<div data-section-style="11" style="max-width:100%">![](https://quip.com/blob/VCCAAAgSiOv/bCg0Y7SM1ltk55C8QcJWbQ?a=19fd5fK9ohB1hau6vXGCvPPhIonQC1aZfimaz8YLeGAa)</div>

## Practice

**Review: List Operators in Python**  

<pre id="VCCACAPz7VL">list.append(x)  

list.extend(L)  
  equivalent to a[len(a):] = L.  

list.insert(i, x)  
 The first argument is the index of the element before which to insert  
 so a.insert(0, x) inserts at the front of the list,   
 and a.insert(len(a), x) is equivalent to a.append(x).  

list.remove(x)  
 Remove the first item from the list whose value is x.   
 It is an error if there is no such item.  

list.pop([i])  
 Remove the item at the given position in the list, and return it.   
 If no index is specified, a.pop() removes and returns the last item in the list.  

list.index(x)  
 Return the index in the list of the first item whose value is x.   
 It is an error if there is no such item.  

list.count(x)  
 Return the number of times x appears in the list.  

list.sort(cmp=None, key=None, reverse=False)  
 Sort the items of the list in place   
 (the arguments can be used for sort customization,   
   see sorted() for their explanation).  

list.reverse()  
 Reverse the elements of the list, in place. which equals to list[::-1]  

collections.deque.append(x)  
 Add x to the right side of the deque.  

collections.deque.appendleft(x)  
 Add x to the left side of the deque.  

collections.deque.clear()  
 Remove all elements from the deque leaving it with length 0.  

collections.deque.count(x)  
 Count the number of deque elements equal to x.  

collections.deque.extend(iterable)  

collections.deque.extendleft(iterable)  

collections.deque.index(x[, start[, stop]])  
 Returns the first match or raises ValueError if not found.  

`colle`ctions.deque.pop()  

collections.deque.popleft()  

collections.deque.remove(value)  
 Remove the first occurrence of value. If not found, raises a ValueError.  

collections.deque.reverse()  
 Reverse the elements of the deque in-place and then return None.</pre>

**Q1: Add Two Numbers II**  
You are given two **non-empty** linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.  
You may assume the two numbers do not contain any leading zero, except the number 0 itself.  

<pre id="VCCACAROX7i">**Input:** (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)  
**Output:** 7 -> 8 -> 0 -> 7</pre>

<pre id="VCCACA4ROF7"># Definition for singly-linked list.  
# class ListNode(object):  
#     def __init__(self, x):  
#         self.val = x  
#         self.next = None  

class Solution(object):  
    def lsize(self, l):  
        n = 0  
        while l:  
            l = l.next  
            n += 1  
        return n  

    def reverse_lst(self, l):  
        prev = None  
        cur  = l  
        while cur:  
            cur_next = cur.next  
            cur.next = prev  
            prev = cur  
            cur = cur_next  
        return prev  

    def addTwoNumbers(self, l1, l2):  
        """  
        :type l1: ListNode  
        :type l2: ListNode  
        :rtype: ListNode  
        """  
        m, n = self.lsize(l1), self.lsize(l2)  
        if m < n:  
            return self.addTwoNumbers(l2, l1)  

        reversed_l1, reversed_l2 = self.reverse_lst(l1), self.reverse_lst(l2)  
        l1_dummy             = <u>_**ListNode(0)**_</u>  
        l1.next              = l1_dummy  
        l_cur,r_cur          = reversed_l1, reversed_l2  
        carry                = 0  

        <u>_**while l_cur:**_</u>  
            <u>_**if r_cur:**_</u>  
                <u>_**l_cur**_</u><u>_**.val += (r_cur.val + carry)**_</u>  
                <u>_**r_cur** _</u><u>_**= r_cur.next**_</u>  
            <u>_**else:**_</u>  
                <u>_**l_cur**_</u><u>_**.val += carry**_</u>  

            carry     = l_cur.val // 10  
            l_cur.val = l_cur.val % 10  
            l_cur = l_cur.next  

        if l1_dummy.val == 0:  
            l1.next = None  

        return self.reverse_lst(reversed_l1)</pre>

<pre id="VCCACAh5ZIX">**from** collections **import** Counter  

**"""****1\. Given an array and a target, return the number of pairs whose   
sum is the target.****10/12/2018 21:00****Idea: For special cases, list example  
 and calculate the correct answer by math.  
 ****https://www.geeksforgeeks.org/count-pairs-with-given-sum/****"""  

 **_# [1, 2, 4, 5, 3, 1, 2, 0] t = 4 => (4, 0), (3, 1), (3, 1), (2, 2)  
 _print(**"1\. count_pair (dict)"**)  

**def** count_pair(nums, t):  
    count_dict = Counter(nums)  

    _# say t = 4, there are 5 times of 2__    # first 2, pair with other 4 times of 2__    # second 2, pair with other 3 times of 2__    # ....__    # (5 - 1) + .... + 0__    # (5 - 1) * 5 // 2_res = 0    **for** n **in** nums:  
        res += count_dict[t - n]  
        **if** 2 * n == t:  
            res -= 1    **return** res // 2print(count_pair([1, 2, 4, 5, 3, 1, 2, 0], 4))  

print()  

**"""****2\. Given nums and v, return index i where i is the largest index for nums[i] <= v****"""**print(**"2\. get_lower_bound"**)  

**def** get_lower_bound(nums, v):  
    _# return index i where i is the smallest index for nums[i] >= v__     
    # just use l__      
    # nums is sorted__      
    # [1, 2, 3, 4, 5]__      
    # v = 3 -->__      
    #  l = 2 (pointing 3 which is just >= v),__      
    #  r = 1 (pointing 2, which is pointing the last element < v)__      
    # [1, 2, 3, 3, 5]__      
    # v = 3 -->__      
    #  l = 2 (pointing 3 which is just >= v),__      
    #  r = 1 (pointing 2, which is pointing the last element < v)__      
    # [1, 2, 3, 3, 5]__      
    # v = 4__      
    #  l = 4 (pointing 5 which is just > v),__      
    #  r = 3 (pointing 3, which is pointing the last element < v)__      
    # [1, 2, 3, 3, 5]__      
    # v = 6__      
    #  l = 5 (OUT OF BOUND),__      
    #  r = 4 (pointing 3, which is pointing the last element < v)__      
    # [1, 2, 3, 3, 5]__      
    # v = 0__      
    #  l = 0 (pointing 5 which is just >= v),__      
    #  r = -1 (OUT OF BOUND)__      
    # [1, 2, 3, 3, 5]__      
    # v = 1__      
    #  l = 0 (pointing 2 which is just >= v),__      
    #  r = -1 (OUTOFBOUND, which is pointing the last element < v)__      
    # [1, 2, 3, 3, 5]__      
    # v = 5__      
    #  l = 4__      
    #  r = 3 (which is pointing the last element < v)__      
    #  _n = len(nums)  
    l = 0    r = n - 1    **while** l <= r:  
        mid = (l + r) // 2          
        _# mid keeps increasing, 0 <= mid <= n - 1_**if** nums[mid] < v: _# !!! <_l = mid + 1          
              **else**:  
            r = mid - 1      
    **return** l, r  

print(get_lower_bound([1, 2, 3, 4, 5], 3))  
print(get_lower_bound([1, 2, 3, 3, 5], 3))  
print(get_lower_bound([1, 2, 3, 3, 5], 4))  
print(get_lower_bound([1, 2, 3, 3, 5], 6))  
print(get_lower_bound([1, 2, 3, 3, 5], 0))  
print(get_lower_bound([1, 2, 3, 3, 5], 1))  
print(get_lower_bound([1, 2, 3, 3, 5], 5))  

print()  
**"""****2\. Given nums and v, return index i where i is the largest index for nums[i] <= v****"""**print(**"3\. get_upper_bound"**)  
**def** get_upper_bound(nums, v):  
    _# return index i where i is the largest index for nums[i] <= v__    # just use r__    # nums is sorted__    # [1, 2, 3, 4, 5]__    # v = 3 -->__    #  l = 3 (pointing 4 which is just > v),__    #  r = 2 (pointing 3, which is pointing the last element <= v)__    # [1, 2, 3, 3, 5]__    # v = 3 -->__    #  l = 4 (pointing 5 which is just > v),__    #  r = 3 (pointing 3, which is pointing the last element <= v)__    # [1, 2, 3, 3, 5]__    # v = 4__    #  l = 4 (pointing 5 which is just > v),__    #  r = 3 (pointing 3, which is pointing the last element <= v)__    # [1, 2, 3, 3, 5]__    # v = 6__    #  l = 5 (OUT OF BOUND),__    #  r = 4 (pointing 3, which is pointing the last element <= v)__    # [1, 2, 3, 3, 5]__    # v = 0__    #  l = 0 (pointing 5 which is just > v),__    #  r = -1 (OUT OF BOUND)__    # [1, 2, 3, 3, 5]__    # v = 1__    #  l = 1 (pointing 2 which is just > v),__    #  r = 0__    # [1, 2, 3, 3, 5]__    # v = 5__    #  l = 5__    #  r = 4_n = len(nums)  
    l = 0    r = n - 1    **while** l <= r:  
        mid = (l + r) // 2        _# mid keeps increasing, 0 <= mid <= n - 1_**if** nums[mid] <= v: _#!!! <=_l = mid + 1        **else**:  
            r = mid - 1    **return** l, r  

print(get_upper_bound([1, 2, 3, 4, 5], 3))  
print(get_upper_bound([1, 2, 3, 3, 5], 3))  
print(get_upper_bound([1, 2, 3, 3, 5], 4))  
print(get_upper_bound([1, 2, 3, 3, 5], 6))  
print(get_upper_bound([1, 2, 3, 3, 5], 0))  
print(get_upper_bound([1, 2, 3, 3, 5], 1))  
print(get_upper_bound([1, 2, 3, 3, 5], 5))  

print()  

**"""****4\. Binary Search binary_search (nums, target)****"""****def** binary_search(nums, target):  
    n = len(nums)  
    l = 0    r = n - 1 _# use the get_upper_bound template_**while** l <= r:  
        mid = (l + r) // 2        **if** nums[mid] <= target:  
            l = mid + 1        **else**:  
            r = mid - 1    **if** r < 0 **or** nums[r] != target: **return** -1 _# !!!!!!_**return** r  

print(**"4\. binary_search"**)  
print()  

**"""****5\. return [start, end] such that if the range is sorted, then the whole array is sorted.** **[1, 2, 3, 5, 4, 6, 7] => [3, 4]** **[1, 2, 3, 6, 1, 2, 5] => [1, 6]****[1, 2, 3, 6, 3, 2, 5, 7, 6] => [2, 8]****https://www.geeksforgeeks.org/minimum-length-unsorted-subarray-sorting-which-makes-the-complete-array-sorted/****Idea: Base Case -> Improve Time Complexity****What if not exists -- -1****Base Solution: O(n*logn) by sorting****"""**_# get_range([1, 2, 3, 5, 4, 6, 7, 8, 9, 7, 10])  # [2, 4]_print(**"5\. get_range"**)  

**def** get_range(nums):  
    n = len(nums)  
    range_l = -1    range_r = -1    max_sofar = nums[0]  

    **for** i, num **in** enumerate(nums):  
        **if** num < max_sofar:  
            _# unsorted starting at i_**if** range_l == -1:  
                range_l = get_upper_bound(nums, min(nums[i:]))[0]  
            range_r = i  
        **else**:  
            max_sofar = num  
    **return** range_l, range_r  

print(get_range([1, 2, 3, 5, 4, 6, 7]))  
print(get_range([1, 2, 3, 6, 1, 2, 5]))  
print(get_range([1, 2, 3, 6, 3, 2, 5, 7, 6]))  
print(get_range([10, 12, 20, 30, 25, 40, 32, 31, 35, 50, 60])) _# (3\. 8)_print()</pre>

<pre id="VCCACAkl9vn">  
"""  
6\. Find the integer x appears more than n/k times in a sorted array of n integers.   
Return None if not exists  

Test Cases Build:  
[1, 2, 3, 4]  
[1, 2, 3, 4, 5, 6, 6]  
[1, 2, 2, 4, 5, 6, 6]  
[1, 2, 2, 4, 6, 6, 7]  

Found out there might be multiple solutions -> return a list of solutions  
1\. 对于满足条件的数，一定只会出现在0, 1 * length / k, 2 * length / k, 3 * length / k, ... , min( k * length / k, length - 1), 注意最后的边界要取一个较小值。  
2\. 对于条件2中的数字，利用二分法找到第一个出现的位置和最后一个出现的位置，只要次数 >= length / k，就加入到结果中。  

s = n // 4  

Utilize the properity "sorted" to help solving the problem.  
--> What difference will make if the array is sorted.  

"""  

print("6\. find_popular (binary search)")  

def find_first(items, i, j, n):  
    # find the first idx of occurance  
    first = -1  
    while i <= j:  
        mid = (i + j) >> 1  
        if items[mid] < n:  
            i = mid + 1  
        elif items[mid] == n:  
            first = mid  
            j = mid - 1  
        else:  
            j = mid - 1  
    return first  

def find_last(items, i, j, n):  
    # find the last idx of occurance  
    last = -1  
    while i <= j:  
        mid = (i + j) >> 1  
        if items[mid] < n:  
            i = mid + 1  
        elif items[mid] == n:  
            last = mid  
            i = mid + 1  
        else:  
            j = mid - 1  
    return last  

# First Implementation: find at most 2*k points  
# 2*k*log(n)  

def find_popular(nums, k):  
    n = len(nums)  
    res_set = set()  
    freq = n // k  
    bounds = [i * freq for i in range(2 * k) if i * freq <= n - 1]  
    # add right-most boundary  
    # bounds.append(n - 1)  
    candidates = [nums[i] for i in bounds]  
    for i in range(1, len(candidates) - 1):  
        first = find_first(nums, bounds[i - 1], bounds[i], candidates[i])  
        last = find_last(nums, bounds[i], bounds[i + 1], candidates[i])  
        # because boundaries are included  
        # candidate must be found  
        if last - first + 1 > freq:  
            # we use set because candidates may be the same  
            res_set.add(candidates[i])  
    return res_set  

print(find_popular([1, 2, 2, 4, 6, 6, 7], 4)) # {2, 6}  
print(find_popular([1, 2, 2, 4, 6, 7, 7], 4)) # {2, 7}  

# Second Implementation: find at most 2*k points  
# 2*k*(2*k)  
# For each point, look around the k before and k after points.  

print()  

"""  
Merge sort without recursion  
"""  

print("7\. Iterative Merge Sort")  

print()  

"""  
Merge sort without recursion  
"""  

print("8\. Rotate Matrix (matrix)")  
class Solution(object):  
    def rotate(self, matrix):  
        """  
        :type matrix: List[List[int]]  
        :rtype: void Do not return anything, modify matrix in-place instead.  
        """  
        for row in range(len(matrix) / 2):  
            for column in range((len(matrix) + 1)/ 2):  
                a = matrix[row][column]  
                b = matrix[column][len(matrix) - 1 - row]  
                c = matrix[len(matrix) - 1 - row][len(matrix) - 1 - column]  
                d = matrix[len(matrix) - 1 - column][row]  
                matrix[row][column] = d  
                matrix[column][len(matrix) - 1 - row] = a  
                matrix[len(matrix) - 1 - row][len(matrix) - 1 - column] = b  
                matrix[len(matrix) - 1 - column][row] = c  

print()  

print("9\. K Inverse Pairs Array (DP)")  

def kInversePairs(n, k):  
    """  
    n = 1  
    [1]  

    n = 2  
    [1, 2] [2, 1]  
        k = 1 [2, 1]  

    n = 3  
    [1, 2, 3] [1, 3, 2], [2, 1, 3], [2, 3, 1], [3, 1, 2], [3, 2, 1]  
        k = 1  [1,3,2]   and [2,1,3]  
        k = 1  [3, 1, 2] and [2,3,1]  

    n = 4  
        k = 3  
    [3, 2, 1\. 4], [3, 1, 4, 2], [2, 3, 4, 1],  [1, 4, 3, 2]. [2, 4, 1, 3], [4, 1, 2, 3],  
    [4, 1, 3, 2], [4, 3, 1, 2] (5 pairs), [4, 3, 2, 1] (6 pairs)  
    kInversePairs(self, n, k) =  
        kInversePairs(n, k - 1) + kInversePairs(n - 1, k)  

    P(n,r) = n! / (n−r)!  
    C(n,r) = n! / ((n−r)! * r!)  

    """  
    states = [1] + [0] * k # for n = 0, [0, k] pairs  
    for i in range(1, n + 1):  
        next_states = [1] + [0] * k  
        for j in range(1, k + 1):  
            next_states[j] = next_states[j - 1] + states[j]  
            if j - 1 - (i - 1) >= 0:  
                next_states[j] -= states[j - 1 - (i - 1)]  
        states = next_states  
    return states[k] % (10 ** 9 + 7)  

def kInversePairsComplex(n, k):  
    """  
    :type n: int  
    :type k: int  
    :rtype: int  
    """  
    max_k = n * (n - 1) // 2  
    if k > max_k: return 0  
    # states = [[0 for _ in range(max_k + 1)] for _ in range(n + 1)]  
    states = [[0 for _ in range(max_k + 1)] for _ in range(2)]  

    cur_row = 0  
    states[0][0] = 1  

    for i in range(1, n + 1):  
        new_row = (cur_row + 1) % 2  
        states[new_row][0] = 1  
        for j in range(1, min(i * (i - 1) // 2 + 1, k + 1)):  
            # states[new_row][j] = sum([states[cur_row][k] for k in range((j - i + 1), j + 1)])  
            states[new_row][j] = states[new_row][j - 1] - states[cur_row][j - 1 - (i - 1)] + states[cur_row][j]  
        cur_row = new_row  
    return states[cur_row][k] % (10 ** 9 + 7)  

print()  

print("10\. Longest Consecutive Sequence (Set / Union Find)")  

from collections import Counter  

class Solution:  
    def longestConsecutive(self, nums):  
        nums_set = set(nums)  
        res = 0  
        for num in nums:  
            cluster_size = 0  
            n = num  
            while True:  
                if n in nums_set:  
                    nums_set.remove(n)  
                else:  
                    break  
                cluster_size += 1  
                n -= 1  
            n = num + 1  
            while True:  
                if n in nums_set:  
                    nums_set.remove(n)  
                else:  
                    break  
                cluster_size += 1  
                n += 1  
            res = max(res, cluster_size)  
        return res  

    """  
    Complexity of union-find with path-compression, without rank.   
    Union by rank without path compression  
         gives an amortized time complexity of O (log n)  
    Union by rank with path compression  
         gives an amortized time complexity of O(1) < < O(logn)  
    """  

    def find(self, x):  
        y = x  
        while self.parents[y] != y:  
            y = self.parents[y]  
        self.parents[x] = y  
        return y  

    def union(self, x, y):  
        parent_x = self.find(x)  
        parent_y = self.find(y)  
        if parent_x != parent_y:  
            self.parents[parent_x] = parent_y  

    def longestConsecutiveUnionFind(self, nums):  
        """  
        :type nums: List[int]  
        :rtype: int  
        """  
        nums = list(set(nums))  
        self.parents = dict(zip(nums, nums))  
        for num in nums:  
            if num - 1 in self.parents:  
                self.union(num - 1, num)  
            if num + 1 in self.parents:  
                self.union(num + 1, num)  
        count = Counter([self.find(n) for n in nums])  
        return max(count.values() or [0])  

print()</pre>

<pre id="VCCACAikRh8"># Python merge sort in place, so space complexity is O(1)  

def merge_sort(xs):  
    """Inplace merge sort of array without recursive. The basic idea  
    is to avoid the recursive call while using iterative solution.   
    The algorithm first merge chunk of length of 2, then merge chunks  
    of length 4, then 8, 16, .... , until 2^k where 2^k is large than   
    the length of the array  
    """  

    unit = 1  
    while unit <= len(xs):  
        h = 0  
        for h in range(0, len(xs), unit * 2):  
            l, r = h, min(len(xs), h + 2 * unit)  
            mid = h + unit  
            # merge xs[h:h + 2 * unit]  
            p, q = l, mid  
            while p < mid and q < r:  
                if xs[p] < xs[q]: p += 1  
                else:  
                    tmp = xs[q]  
                    xs[p + 1: q + 1] = xs[p:q]  
                    xs[p] = tmp  
                    p, mid, q = p + 1, mid + 1, q + 1  
        unit *= 2  

    return xs</pre>
