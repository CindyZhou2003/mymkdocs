## Leetcode

### Easy
#### Maximurn SubArray
最大字串
```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        vector<vector<int>> dp(2, vector<int>(size(nums)));
        dp[0][0] = dp[1][0] = nums[0];
        for(int i = 1; i < size(nums); i++) {
            dp[1][i] = max(nums[i], nums[i] + dp[1][i-1]);
            dp[0][i] = max(dp[0][i-1], dp[1][i]);
        }
        return dp[0].back();//返回对向量末端元素的引用
    }
};
```
We can actually do away with just 1 row as well. We denoted `dp[1][i]` as the maximum subarray sum ending at `i`. We can just store that row and calculate the overall maximum subarray sum at the end by choosing the maximum of all max subarray sum ending at `i`.
```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        vector<int> dp(nums);
        for(int i = 1; i < size(nums); i++) 
            dp[i] = max(nums[i], nums[i] + dp[i-1]);        
        return *max_element(begin(dp), end(dp));
    }
};
```
#### 169.Major Element

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int l=nums.size();
        int count=1, major=nums[0];
        for(int i=1;i<l;i++){
            if(count==0) major=nums[i];//count=0说明有另一个数出现的次数大于原来的
            if(nums[i]==major)count++;
            else count--;
        }
        return major;
    }
};
```



### Two sum

**暴力破解**
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int n = nums.size();
        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {
                if (nums[i] + nums[j] == target) {
                    return {i, j};
                }
            }
        }
        return {}; // No solution found
    }
};
```
**两遍哈希表**
```cpp
class Solution {
public:
    	vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> numMap;
        int n = nums.size();

        // Build the hash table
        for (int i = 0; i < n; i++) {
            numMap[nums[i]] = i;
        }

        // Find the complement
        for (int i = 0; i < n; i++) {
            int complement = target - nums[i];
            if (numMap.count(complement) && numMap[complement] != i) {
                return {i, numMap[complement]};
            }
        }

        return {}; // No solution found
    }
};
```
**单哈希表**
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> numMap;
        int n = nums.size();

        for (int i = 0; i < n; i++) {
            int complement = target - nums[i];
            if (numMap.count(complement)) {
                return {numMap[complement], i};
            }
            numMap[nums[i]] = i;
        }

        return {}; // No solution found
    }
};
```
### Construct Binary Tree from Inorder and Postorder Traversal
```cpp
class Solution {
public:
    unordered_map<int,int>ump;
//This map is used to store the indices of elements in the inorder vector for quick lookup.

    TreeNode* build(vector<int>& inorder, vector<int>& postorder,int &rootIdx,int left,int right)
    {
        if(left>right)
        {
            return NULL;
        }
        
 		int pivot=ump[postorder[rootIdx]];
        
        rootIdx--;
        TreeNode* node=new TreeNode(inorder[pivot]);
        
        node->right=build(inorder,postorder,rootIdx,pivot+1,right);
        
        node->left=build(inorder,postorder,rootIdx,left,pivot-1);
        
        return node;
    }
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        
        int rootIdx=postorder.size()-1;
        for(int i=0;i<inorder.size();i++)
        {
            ump[inorder[i]]=i;
        }
        
        return build(inorder,postorder, rootIdx, 0, inorder.size()-1);
        
    }
};
```
### Binary Tree Zigzag Level Order Traversal
### Median of two sorted arrays
**暴力破解**
```cpp
class Solution {
public:
double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
    // Get the sizes of both input arrays.
    int n = nums1.size();
    int m = nums2.size();

    // Merge the arrays into a single sorted array.
    vector<int> merged;
    for (int i = 0; i < n; i++) {
        merged.push_back(nums1[i]);
    }
    for (int i = 0; i < m; i++) {
        merged.push_back(nums2[i]);
    }

    // Sort the merged array.
    sort(merged.begin(), merged.end());

    // Calculate the total number of elements in the merged array.
    int total = merged.size();

    if (total % 2 == 1) {
        // If the total number of elements is odd, return the middle element as the median.
        return static_cast<double>(merged[total / 2]);
    } else {
        // If the total number of elements is even, calculate the average of the two middle elements as the median.
        int middle1 = merged[total / 2 - 1];
        int middle2 = merged[total / 2];
        return (static_cast<double>(middle1) + static_cast<double>(middle2)) / 2.0;
    }
}
};
```
**二分搜索 **
```cpp
class Solution {
public:
double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
    int m=nums1.size(),n=nums2.size();
    int all=m+n;
    int M= (m+n+1)/2;
    int low=0,high=m;
    if(m>n) return findMedianSortedArrays(nums2,nums1);
    while(low<=high){
        int m1=(low+high)/2;
        int m2=M-m1;
        int l1 = INT_MIN, l2 = INT_MIN, r1 = INT_MAX, r2 = INT_MAX;
        if(m1<m) r1=nums1[m1];//
        if(m2<n) r2=nums2[m2];
        if(m1>=1) l1=nums1[m1-1];//左边中点的左边一个数
        if(m2>=1) l2=nums2[m2-1];
        if(l1<=r2 && l2<=r1){
            if(all%2==1) return max(l1,l2);//找到中间值
            else return (max(l1,l2)+min(r1,r2))/2.0;
        }
        else if(l1>r2) high=m1-1;//nums1向量中点数太大了，要变小
        else low=m1+1;
    }

    return 0;//没找到，输入向量内部未排序
}
};
```
### Longest Palindromic Substring 最长回文串
```c
class Solution {
private: 
    bool isPalindrome(const std::string& str) {
        int left = 0;
        int right = str.length() - 1;
        
        while (left < right) {
            if (str[left] != str[right]) {
                return false;
            }
            ++left;
            --right;
        }
        
        return true;
    }

public:
    string longestPalindrome(string s) {
              if (s.length() <= 1) {
            return s;
        }

        auto expand_from_center = [&](int left, int right) {
            while (left >= 0 && right < s.length() && s[left] == s[right]) {
                left--;
                right++;
            }
            return s.substr(left + 1, right - left - 1);
        };

        std::string max_str = s.substr(0, 1);

        for (int i = 0; i < s.length() - 1; i++) {
            std::string odd = expand_from_center(i, i);
            std::string even = expand_from_center(i, i + 1);

            if (odd.length() > max_str.length()) {
                max_str = odd;
            }
            if (even.length() > max_str.length()) {
                max_str = even;
            }
        }

        return max_str;          
    }
};
```
### Medium
#### 55.Jump Game
*You are given an integer array nums. You are initially positioned at the array's first index, and each element in the array represents your maximum jump length at that position. Return true if you can reach the last index, or false otherwise.*

```cpp
class Solution {
public:
    bool canJump(vector<int>& nums) {
        int next,i;
        int s=nums.size();
        if(s==1)return true;
        for(i=0;i<=next;i++){
            next=max(next,nums[i]+i);
            if(next>=s-1) return true;
        }
        return false;
    }
};
```
#### 238.Product of Array Except Self

*Given an integer array `nums`, return an array `answer` such that `answer[i]` is equal to the product of all the elements of `nums` except `nums[i]`.*

My answer: 

- 非零相乘，结果除以自己；有零单个零则0变成其他数相乘；两个零及以上都是零 

- T：O(N)

Others：

```c++
    public int[] productExceptSelf(int[] nums) {
    	int n = nums.length;
    	int[] res = new int[n];
    	int right=1,left=1;
        for(int i=0;i<n;i++){
            res[i]=1;
        }
    	for (int i=0;i<n;i++) {
    		res[i]*=left;
    		left*=nums[i];
    	}
    	for(int i=n-1;i>=0;i--) {
    		res[i]*=right;
    		right*=nums[i];
    	}
    	return res;
    }
```

- 将当前数的左边和右边分别乘起来得到答案
- T：O(N)

#### 240.Search a 2D Matrix Ⅱ

Write an efficient algorithm that searches for a value `target` in an `m x n` integer matrix `matrix`. This matrix has the following properties:

- Integers in each row are sorted in ascending from left to right.
- Integers in each column are sorted in ascending from top to bottom.

*Method: Search from the **top-right** element and reduce the search space by one row or column at each time.*

```c++
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int m = matrix.size(), n=matrix[0].size(),
        int r = 0, c = n - 1;
        while (r < m && c >= 0) {
            if (matrix[r][c] == target) {
                return true;
            }
            matrix[r][c] > target ? c-- : r++;
        }
        return false;
    }
};
```



#### 80.Remove Duplicates From Sorted Array2

```cpp
class Solution {
public:
int removeDuplicates(vector<int>& nums) {
	int i = 0;
	for (int n : nums)
		if (i < 2 || n > nums[i-2])
			nums[i++] = n;
	return i;
}
};
//最多出现两个重复的是2， 最多有k个重复的就把2改成k
```
#### 189.Rotate Array

```cpp
class Solution {
public:
void rotate(vector<int>& nums, int k) {
    int l=nums.size();
    if(k>l) k=k%l;
    reverse(nums.begin(),nums.end());
    reverse(nums.begin(),nums.begin()+k);
    reverse(nums.begin()+k,nums.end());
}     
```
### Hard

#### 239.Sliding window maximum

You are given an array of integers `nums`, there is a sliding window of size `k` which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position.

Return *the max sliding window*.

Time complexity：O(N)

```c++
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        int n = nums.size();
        vector<int> windowMax;
        deque<int> dq;
        for (int i = 0; i < n; i++) {
            while (!dq.empty() && dq.front() < i - k + 1)//dp.front()是第一个元素
                dq.pop_front();// Removes the first element
            while (!dq.empty() && nums[dq.back()] < nums[i])
                dq.pop_back();// Removes the last element
            dq.push_back(i);
            if (i >= k - 1) windowMax.push_back(nums[dq.front()]);
        }
        return windowMax;
    }
};
```



## OTHER

### Check if a given Binary Tree is height balanced like a Red-Black Tree
```c
bool isBalancedUtil(struct node* root, int* maxh, int* minh) {
    // Base case
    if (root == NULL) {
        *maxh = *minh = 0;
        return true;
    }

    int lmxh, lmnh; // max and min heights of the left subtree
    int rmxh, rmnh; // max and min heights of the right subtree

    // Check if the left subtree is balanced, also set lmxh and lmnh
    if (isBalancedUtil(root->left, &lmxh, &lmnh) == false)
        return false;

    // Check if the right subtree is balanced, also set rmxh and rmnh
    if (isBalancedUtil(root->right, &rmxh, &rmnh) == false)
        return false;

    // Set the max and min heights of this node for the parent call
    *maxh = (lmxh > rmxh ? lmxh : rmxh) + 1;
    *minh = (lmnh < rmnh ? lmnh : rmnh) + 1;

    // See if this node is balanced
    if (*maxh <= 2 * *minh)
        return true;

    return false;
}

// A wrapper over isBalancedUtil()
bool isBalanced(struct node* root) {
    int maxh, minh;
    return isBalancedUtil(root, &maxh, &minh);
}
```
