# Leetcode

[TOC]

$解答来自Leetcode$

## 按题号

### 6 Z字形变换

题意：将一个字符串的字母以Z字形排列

难度：中等

方法：每个字符 `c` 在 N 字形中对应的 **行索引** 先从 *s*1 增大至 $s_n$，再从 $s_n$ 减小至 *s*1

```c++
class Solution {
public:
    string convert(string s, int numRows) {
        if (numRows < 2)
            return s;
        vector<string> rows(numRows);
        int i = 0, flag = -1;
        for (char c : s) {
            rows[i].push_back(c);// 把每个字符c填入对应行si
            if (i == 0 || i == numRows -1)
                flag = - flag;
            // 在达到 Z 字形转折点时，执行反向
            
            i += flag;// 更新当前字符 c 对应的行索引
        }
        string res;
        for (const string &row : rows)
            res += row;
        return res;
    }
};
```

### 7 整数反转

题意：rt，注意是否溢出

难度：中等

方法：

```c++
class Solution {
public:
    int reverse(int x) {
        int b,flag=1;
        if(x==0){
            return 0;
        }
        int res = 0;
        while(x!=0){
            if (res < INT_MIN / 10 || res > INT_MAX / 10) {// 判断是否溢出
                return 0;
            }
            b=x%10;
            res=res*10+b;
            x=x/10;
        }

        return res;
    }
};

//JAVA 可以抛出异常解决溢出
```

### 8 字符串转换整数 (atoi)

题意：rt，去除先导空格，0，判断正负，遇到非数字返回0

难度：中等

**方法（直接做）**：

```c++
class Solution {
public:
    int myAtoi(string s) {
        if(s.empty())return 0;

        // 跳过前导空格
        int i = 0, n = s.length(), num=0;
        while (i < n && s[i] == ' ') i++;

        // 判断正负，flag 用于最后与 num 相乘作为结果
        int flag = 1; // 无符号时为 1 (正)
        if ( i<n && (s[i] == '-' || s[i] == '+')) {
            flag = s[i]=='+'? 1:-1;
            i++;
        }

        // 跳过前导 0 
        while (i < n && s[i] == '0') i++;
        if (i == n) return 0;

        // 开始读取数字
        for (; i < n; i++) {
            char c = s[i];
            int digit = c - '0';
            // 遇到除数字外的字符退出
            if (c < '0' || c > '9') break;
            
            // 判断是否溢出
            if(num>(INT_MAX - digit)/10){
                return flag == 1? INT_MAX : INT_MIN;
            }
            // 得到无符号的新数字
            num = num * 10 + digit;
        }
        return num * flag;
    }
};
```

### 10 正则表达式匹配

题意：详见[10. 正则表达式匹配 - 力扣（LeetCode）](https://leetcode.cn/problems/regular-expression-matching/solutions/296114/shou-hui-tu-jie-wo-tai-nan-liao-by-hyj8/)

难度：困难

**方法（动态规划）**：

```c++
class Solution {
public:
    bool isMatch(string s, string p) {
        int lens=s.size();
        int lenp=p.size();
        vector<vector<bool>> dp(lens+1,vector<bool>(lenp+1,false));
        //因为包含了空字串的情况
        //初始化 
        dp[0][0]=true;//两个空字串
        for(int j=1;j<lenp+1;j++){
            //找出s为空 但p因为*为空的情况
            if(p[j-1]=='*'){
                dp[0][j]=dp[0][j-2];
            }
        }
        //更新
        for(int i=1;i<lens+1;i++){
            for(int j=1;j<lenp+1;j++){
                if(s[i-1]==p[j-1] || p[j-1]=='.'){
                    dp[i][j]=dp[i-1][j-1];//情况1：符合，直接更新
                }
                else if(p[j-1]=='*'){
                    //情况2：考虑*的情况
                    if(s[i-1]==p[j-2]||p[j-2]=='.'){
                        dp[i][j]=dp[i][j-2]||dp[i-1][j-2]||dp[i-1][j];
               //分别是 重复0次；重复一次；重复两次及以上！！！
                    }
                    else{//s[i-1] p[j-2]不匹配  *需要重复0次
                        dp[i][j]=dp[i][j-2];
                    }
                }
            }
        }
        return dp[lens][lenp];
    }
};
```

### 15 三数之和

题意：给定一个数组，要求在这个数组中找出 3 个数之和离 target 最近。

难度：中等

**方法：排序+双指针移动**

```cpp
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        sort(nums.begin(), nums.end());//排序
        int n = nums.size();
        int best = 1e7;

        // 根据差值的绝对值来更新答案
        auto update = [&](int cur) {
            if (abs(cur - target) < abs(best - target)) {
                best = cur;
            }
        };

        // 枚举 a
        for (int i = 0; i < n; ++i) {
            // 保证和上一次枚举的元素不相等
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            // 使用双指针枚举 b 和 c
            int j = i + 1, k = n - 1;
            while (j < k) {
                int sum = nums[i] + nums[j] + nums[k];
                // 如果和为 target 直接返回答案
                if (sum == target) {
                    return target;
                }
                update(sum);
                if (sum > target) {
                    // 如果和大于 target，移动 c 对应的指针
                    int k0 = k - 1;
                    // 移动到下一个不相等的元素
                    while (j < k0 && nums[k0] == nums[k]) {
                        --k0;
                    }
                    k = k0;
                } else {
                    // 如果和小于 target，移动 b 对应的指针
                    int j0 = j + 1;
                    // 移动到下一个不相等的元素
                    while (j0 < k && nums[j0] == nums[j]) {
                        ++j0;
                    }
                    j = j0;
                }
            }
        }
        return best;
    }
};
```



### 18 四数之和

题意：类似 [15 三数之和](# 15 三数之和)

难度：中等

**方法：排序+双指针**

- 时间复杂度：O(n^3^)，其中 n 是数组的长度。排序的时间复杂度是O(nlogn)，枚举四元组的时间复杂度是 O(n^3^)，因此总时间复杂度为 O(n^3^ +nlogn)=O(n^3^)。

- 空间复杂度：O(logn)，其中 n 是数组的长度。空间复杂度主要取决于排序额外使用的空间。此外排序修改了输入数组 nums，实际情况中不一定允许，因此也可以看成使用了一个额外的数组存储了数组 nums 的副本并排序，空间复杂度为 O(n)。

```cpp
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        vector<vector<int>> ans;
        int n = nums.size();
        sort(nums.begin(), nums.end());
        for (int i = 0; i < n - 3; ++i) {
            if (i > 0 && nums[i] == nums[i-1]) continue;
            if ((long)nums[i] + nums[i+1] + nums[i+2] + nums[i+3] > target) break;
            if ((long)nums[i] + nums[n-1] + nums[n-2] + nums[n-3] < target) continue;

            for (int j = i + 1; j < n - 2; ++j) {
                if (j > i + 1 && nums[j] == nums[j-1]) continue;
                if ((long)nums[i] + nums[j] + nums[j+1] + nums[j+2] > target) break;
                if ((long)nums[i] + nums[j] + nums[n-2] + nums[n-1] < target) continue;

                int l = j + 1, r = n - 1;
                while (l < r) {
                    long value = (long)nums[i] + nums[j] + nums[l] + nums[r];
                    if (value < target) {
                        ++l;
                    } else if (value > target) {
                        --r;
                    } else {
                        ans.push_back({nums[i], nums[j], nums[l], nums[r]});
                        while (l < r && nums[l] == nums[++l]);
                        while (r > l && nums[r] == nums[--r]);
                    }
                }
            }
        }
        return ans;
    }
};
```



### 19 删除链表倒数第n个节点

题意：rt

难度：中等

**方法1**：计算链表长度，创建临时指针（要delete）连接

- 时间复杂度：*O*(*L*)，其中 *L* 是链表的长度
- 空间复杂度：*O*(1)

**方法2**：递归，达到终止条件后，每执行一次返回，++count，把第n个节点跳过

- 时间复杂度：*O*(*L*)，其中 *L* 是链表的长度
- 空间复杂度：*O*(1)（没有）

方法3：双指针，一个先遍历n次，后一起遍历，创建临时指针（要delete）连接

- 时间复杂度：*O*(*L*)，其中 *L* 是链表的长度。
- 空间复杂度：*O*(1)。

### 20 有效的括号

题意：3种括号，左括号必须以正确的顺序闭合

难度：简单

**方法**：map匹配+栈

```c++
bool isValid(string s) {
    int n=s.size();
    if(n%2==1)return false;
    unordered_map<char,char>pair={{')','('},{']','['},{'}','{'}};//匹配时右边先
    stack<char>stk;
    for(char ch :s){
        if(pair.count(ch)){//如果Map中存在具有给定键的值，则此函数返回1，否则返回0,即是右括号的情况
            if(stk.empty()||stk.top()!=pair[ch]) return false;
            //如果碰到了一个括号，但栈里是空的或者顶端的元素不是对应括号，返回false
            stk.pop();//匹配成功，弹出栈顶元素
        }else stk.push(ch);//左括号情况，直接加入栈
    }
    return stk.empty();
}
```

### 21 合并两个有序链表

题意：升序排列

难度：简单

**方法1**：递归（函数递归）

```c++
ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
    if(list1==nullptr)return list2;
    if(list2==nullptr)return list1;
    if(list1->val<list2->val){
        list1->next=mergeTwoLists(list1->next,list2);
        return list1;
    }else{
        list2->next=mergeTwoLists(list1,list2->next);
        return list2;
    }
}
```

- 时间复杂度：O(n+m)，其中 n 和 m 分别为两个链表的长度。因为每次调用递归都会去掉 l1 或者 l2 的头节点（直到至少有一个链表为空），函数 mergeTwoList 至多只会递归调用每个节点一次。因此，时间复杂度取决于合并后的链表长度，即 O(n+m)。

- 空间复杂度：O(n+m)，其中 n 和 m 分别为两个链表的长度。递归调用 mergeTwoLists 函数时需要消耗栈空间，栈空间的大小取决于递归调用的深度。结束递归调用时 mergeTwoLists 函数最多调用 n+m 次，因此空间复杂度为 O(n+m)。

**方法2**：迭代

```c++
ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
    ListNode* preHead = new ListNode(-1);//链表头

    ListNode* prev = preHead;//维护prev指针
    while (l1 != nullptr && l2 != nullptr) {
        if (l1->val < l2->val) {
            prev->next = l1;
            l1 = l1->next;
        } else {
            prev->next = l2;
            l2 = l2->next;
        }
        prev = prev->next;
    }
    // 合并后 l1 和 l2 最多只有一个还未被合并完，我们直接将链表末尾指向未合并完的链表
    prev->next = l1 == nullptr ? l2 : l1;

    return preHead->next;
};
```

- 时间复杂度：O(n+m)，其中 n 和 m 分别为两个链表的长度。因为每次循环迭代中，l1 和 l2 只有一个元素会被放进合并链表中， 因此 while 循环的次数不会超过两个链表的长度之和。所有其他操作的时间复杂度都是常数级别的，因此总的时间复杂度为 O(n+m)。

- 空间复杂度：O(1)。我们只需要常数的空间存放若干变量。

### 22 括号生成

题意：生成n种有效的（）组合

难度：中等

**方法**：回溯backtracking，左右括号从 n 开始递减，F(n+1)=(+F(i)+)+F(n-i)

```c++
class Solution {
public:
    vector<string>res;
    vector<string> generateParenthesis(int n) {
        if(n<=0)return res;
        getParenthesis("",n,n);
        return res;
    }
private:
    void getParenthesis(string str, int left, int right){
        if(left==0&&right==0){
            res.push_back(str);//左右括号都为0，结束
            return;
        } 
        //如果左括号还有添加一个左括号
        if(left>0)getParenthesis(str+"(",left-1,right);
        
        //如果剩余的左括号小于右括号，才可以使用右括号，因为括号要想有效一定是先放左后放右的
        if(left<right){
            getParenthesis(str+")",left,right-1);
        }
    }
};
```

### 23 合并K个升序链表

题意：rt

难度：困难

**方法**：优先队列

```c++
// Definition for singly-linked list.(Already given)
struct ListNode {
    int val;
    ListNode *next;
    ListNode() : val(0), next(nullptr) {}
    ListNode(int x) : val(x), next(nullptr) {}
    ListNode(int x, ListNode *next) : val(x), next(next) {}
};

class Solution {
public:
    struct Compare {//链表的比较
        bool operator()(ListNode* a, ListNode* b) {
            return a->val > b->val;
        }
    };
    
    ListNode* mergeKLists(std::vector<ListNode*>& lists) {
        std::priority_queue<ListNode*, std::vector<ListNode*>, Compare> pq;//std::priority_queue<Type, Container, Compare>


        // 将每个链表的头加到优先队列中
        for (auto node : lists) {
            if (node != nullptr) {
                pq.push(node);
            }
        }

        ListNode dummy;// 定义一个空头
        ListNode* cur = &dummy;

        while (!pq.empty()) {
            ListNode* s = pq.top();//优先队列的第一个元素，即min heap中的最小头
            pq.pop();// 将头移出队列
            cur->next = s;// 连接上已部分排序的队列（即要的结果队列）
            cur = cur->next;// 重置结果队列末尾

            if (s->next != nullptr) {
                pq.push(s->next);// 将链表下一个元素加入优先队列
            }
        }

        return dummy.next;
    }
};

```

### 24 两两交换链表中的节点

题意：rt 不能改链表节点值

难度：中等

**方法**：递归，  宗旨就是紧紧抓住原来的函数究竟返回的是什么?作用是什么即可，其余的细枝末节不要细究,编译器会帮我们自动完成

- 时间复杂度：
- 空间复杂度：

```c++
public ListNode* swapPairs(ListNode* head) {
    // base case
    if (head == nullptr || head.next == nullptr) return head;

    // swapPairs(ListNode head) 的意义就是两两翻转链表中的节点+返回翻转后的新的头结点
    // 我们知道翻转后新的头结点必然是第二个节点
    // 举例子:1->2->3->4 翻转后:2->1->4->3
    ListNode* newHead = head->next; // 2
    // 此时tmpHead为:4->3
    ListNode* tmpHead = swapPairs(newHead->next);
    // 而前面的还粘连着:1->2->(3)  4->3
    // 此时再让1->4 此时链表为:2->(3) 1->4->3
    head->next = tmpHead;
    // 再将2指向1即可 此时链表为:2->1->4->3 已经完成翻转
    newHead->next = head;
    // 返回新的头结点
    return newHead;
}
```

### 25 k个一组翻转链表

题意：rt

难度：困难

方法：根据[220 翻转链表](#220 翻转链表)先翻转每组再连接起来

```c++
class Solution {
public:
    // 翻转一个子链表，并且返回新的头与尾，即类似220
    pair<ListNode*, ListNode*> myReverse(ListNode* head, ListNode* tail) {
        ListNode* prev = tail->next;
        ListNode* p = head;
        while (prev != tail) {
            ListNode* nex = p->next;
            p->next = prev;
            prev = p;
            p = nex;
        }
        return {tail, head};
    }

    ListNode* reverseKGroup(ListNode* head, int k) {
        ListNode* hair = new ListNode(0);
        hair->next = head;
        ListNode* pre = hair;

        while (head) {
            ListNode* tail = pre;
            // 查看剩余部分长度是否大于等于 k
            for (int i = 0; i < k; ++i) {
                tail = tail->next;
                if (!tail) {
                    return hair->next;
                }
            }
            ListNode* nex = tail->next;
            // 这里是 C++17 的写法，也可以写成
            // pair<ListNode*, ListNode*> result = myReverse(head, tail);
            // head = result.first;
            // tail = result.second;
            tie(head, tail) = myReverse(head, tail);
            // 把子链表重新接回原链表
            pre->next = head;
            tail->next = nex;
            pre = tail;
            head = tail->next;
        }

        return hair->next;
    }
};
```

### 28 找出字符串中第一个匹配项的下标

题意：rt

难度：简单

**方法1：朴素直接做**

- 时间复杂度：n 为原串的长度，m 为匹配串的长度。其中枚举的复杂度为O(n−m)，构造和比较字符串的复杂度为 O(m)。整体复杂度为O((n−m)∗m)

- 空间复杂度：O(1)

**方法2：KMP**

- 时间复杂度：`n` 为原串的长度，`m` 为匹配串的长度。复杂度为 *O*(*m*+*n*)。
- 空间复杂度：构建了 `next` 数组。复杂度为 *O*(*m*)。

```cpp
vector<int> KMP(const string &text, const string &pattern) {
    int n = text.size(), m = pattern.size();
    vector<int> next(m, 0);//赋值为0
    vector<int> matches;
 /*
 next[i]表示在模式字符串中，pattern[0:i]的前缀和后缀的最长公共部分的长度
对于模式字符串"ABABAC"，next数组为[0, 0, 1, 2, 3, 0]。
next[0] = 0：第一个字符没有前缀和后缀，所以为0
next[1] = 0：到"AB"为止，前缀"A"和后缀"B"没有公共部分，所以为0
next[2] = 1：到"ABA"为止，前缀"A"和后缀"A"的最长公共部分长度为1
以此类推
 */
    for (int i = 1; i < m; i++) {
        int j = next[i - 1];
        while (j > 0 && pattern[i] != pattern[j])
            j = next[j - 1];
        if (pattern[i] == pattern[j])
            j++;
        next[i] = j;
    }

    int j = 0;
    for(int i=0;i<n;i++){
        while (j > 0 && text[i] != pattern[j])
            j = next[j - 1]; // 使用next[j-1]更新j，跳过不必要的比较
        if (text[i] == pattern[j])
            j++;
        if (j == m) {//和要匹配的字符串长度一样，则匹配成功
            //matches.push_back(i - j + 1);
            //j = next[m - 1]; 这是继续寻找下一个匹配位置
            return i-j+1; // 题目只需要返回第一个匹配位置即可
        }
    }
    return -1; // 没有对应匹配的字符串，返回-1
}
```

### 29 两数相除
题意：**不使用** 乘法、除法和取余运算，假设环境只能存储 *32 位* 有符号整数，其数值范围是 [−2^31^, 2^31^ − 1]

难度：中等

方法：循环（递归）

- 时间复杂度：O(log)
- 空间复杂度：O(1)?

```c++
class Solution {
    public int divide(int dividend, int divisor) {
        if(divisor==1) return dividend;
        if(divisor==-1){
            if(dividend==INT_MIN){
                return INT_MAX;
            }
            return -dividend;
        }

        boolean isNeg=(dividend>0 && divisor<0) || (dividend<0 && divisor>0);
        if(dividend>0) dividend=-dividend;
        if(divisor>0) divisor=-divisor;//将正数转化成负数做，防溢出

        int ans = 0;
        while(dividend<=divisor){           
            int a=divisor;
            int temp=1;
            while(dividend-a<=a){
                a+=a;
                temp+=temp;
            }
            ans+=temp;
            dividend=dividend-a;
        }
        return isNeg?-ans:ans;
    }
}
```



### 30 串联所有单词的子串

### 31 下一个排列

题意：给定数字序列的字典序中下一个更大的排列。如果不存在下一个更大的排列，则将数字重新排列成最小的排列（即升序排列）

难度：中等

方法：C++STL方法

1. 从后向前 查找第一个 相邻升序 的元素对 (i,j)，满足 A[i] < A[j]。此时 [j,end) 必然是降序
2. 在 [j,end) 从后向前 查找第一个满足 A[i] < A[k] 的 k。A[i]、A[k] 分别就是上文所说的「小数」、「大数」
3. 将 A[i] 与 A[k] 交换
4. 可以断定这时 [j,end) 必然是降序，逆置 [j,end)，使其升序
5. 如果在步骤 1 找不到符合的相邻元素对，说明当前 [begin,end) 为一个降序顺序，则直接跳到步骤 4

```c++
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        if (nums.size() <= 1) {
            return;
        }
        for (int i = nums.size()-2; i >= 0; --i) {
            if (nums[i] < nums[i + 1]) {//从后往前找第一个相邻升序元素对A[i]<A[i+1]
                for (int j = nums.size() - 1; j > i; --j) {
                    //从[j,end)找第一个A[k]>A[i]
                    if (nums[i] < nums[j]) {
                        swap(nums[i], nums[j]);//交换A[i]和A[k]
                        reverse(nums.begin() + i + 1, nums.end());
                        //[j,end) 必然是降序，逆置 [j,end)，使其升序
                        return;
                    }
                }
            }
        }
        reverse(nums.begin(), nums.end());
        //如果没有提前退出，那么就是没碰到逆序遍历是降序的，全是升序，说明最大了
    }
};
```

### 32 最长有效括号

题意：给你一个只包含 `'('` 和 `')'` 的字符串，找出最长有效（格式正确且连续）括号子串的长度。

难度：困难

**方法1：栈**

- 时间复杂度：O(n)
- 空间复杂度：O(n)，因为栈的大小最多等于字符串的长度

```c++
class Solution {
public:
    int longestValidParentheses(string s) {
        int maxans = 0;
        stack<int> stk;
        stk.push(-1);
        //初始化一个栈，栈中放置一个初始值 `-1`，代表最后一个没有匹配的右括号的索引。
        for (int i = 0; i < s.length(); i++) {
            if (s[i] == '(') {
                stk.push(i);//遇到左括号 `(`，将它的索引压入栈
            } else {
                stk.pop();//遇到右括号 `)`，弹出栈顶元素
                if (stk.empty()) {
                    stk.push(i);//栈为空，说明当前的右括号为没有被匹配的右括号，将它的索引压入栈
                } else {
                    maxans = max(maxans, i - stk.top());
                    //如果栈不为空，计算当前右括号和栈顶的索引差，并更新最长的有效括号长度
                }
            }
        }
        return maxans;
    }
};
```

**方法2：动态规划**

1. 初始化一个 `dp` 数组，大小为字符串长度，初始值全为 0。

2. 遍历字符串：

- 如果当前字符是 `)` 并且前一个字符是 `(`，则我们有一个匹配的括号对，可以将当前 `dp` 值设为 `dp[i-2] + 2`。
- 如果当前字符是 `)` 并且前一个字符是 `)`，则检查前一个位置对应的有效括号长度前面的字符是否为 `(`，如果是，则可以形成一个新的有效子串。

3. 不断更新最长的有效括号长度。

- 时间复杂度：O(n)
- 空间复杂度：O(n)，需要一个数组来记录每个位置的解

```c++
class Solution {
public:
    int longestValidParentheses(string s) {
        int size = s.length();
        vector<int> dp(size, 0);

        int maxVal = 0;
        for(int i = 1; i < size; i++) {
            if (s[i] == ')') {
                if (s[i - 1] == '(') {
                    dp[i] = 2;
                    if (i - 2 >= 0) {
                        dp[i] = dp[i] + dp[i - 2];
                    }
                } else if (dp[i - 1] > 0) {
                    if ((i - dp[i - 1] - 1) >= 0 && s[i - dp[i - 1] - 1] == '(') {
                        dp[i] = dp[i - 1] + 2;
                        if ((i - dp[i - 1] - 2) >= 0) {
                            dp[i] = dp[i] + dp[i - dp[i - 1] - 2];
                        }
                    }
                }
            }
            maxVal = max(maxVal, dp[i]);
        }
        return maxVal;
    }
};
```

### 33 搜索旋转排序数组

题意：要求log(n)时间复杂度内解决，数组已经绕某个数旋转过

难度：中等

**方法：二分法**

```c++
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int l = 0, r = nums.size() -1;
        
        while (l <= r)
        {
            int mid = (l + r)/2;
            if (target == nums[mid]) return mid;

            if (nums[l] <= nums[mid])
            {
                if (target >= nums[l] && target < nums[mid])
                    r = mid-1;
                else
                    l = mid+1;
            }
            else
            {
                if (target > nums[mid] && target <= nums[r])
                    l = mid +1;
                else
                    r = mid -1;
            }
        }
        return -1;
    }
};
```



### 34 在排序数组中查找第一个和最后一个位置

题意：

难度：中等

**方法：二分查找**

- 时间复杂度： O(logn) ，其中 n 为数组的长度。二分查找的时间复杂度为 O(logn)，一共会执行两次，因此总时间复杂度为 O(logn)。

- 空间复杂度：O(1) 。只需要常数空间存放若干变量。

```java
// 两次二分查找，分开查找第一个和最后一个
// 时间复杂度 O(log n), 空间复杂度 O(1)
// [1,2,3,3,3,3,4,5,9]
public int[] searchRange(int[] nums, int target) {
    int left = 0;
    int right = nums.length - 1;
    int first = -1;
    int last = -1;
    // 找第一个等于target的位置
    while (left <= right) {
        int middle = (left + right) / 2;
        if (nums[middle] == target) {
            first = middle;
            right = middle - 1; //重点
        } else if (nums[middle] > target) {
            right = middle - 1;
        } else {
            left = middle + 1;
        }
    }

    // 最后一个等于target的位置
    left = 0;
    right = nums.length - 1;
    while (left <= right) {
        int middle = (left + right) / 2;
        if (nums[middle] == target) {
            last = middle;
            left = middle + 1; //重点
        } else if (nums[middle] > target) {
            right = middle - 1;
        } else {
            left = middle + 1;
        }
    }

    return new int[]{first, last};
}
```





### 167 两个和 II

题意：输入的数组已排序

难度：简单

**方法：双指针**

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```python
public int[] twoSum(int[] numbers, int target) {
    if (numbers == null) return null;
    int i = 0, j = numbers.length - 1;
    while (i < j) {
        int sum = numbers[i] + numbers[j];
        if (sum == target) {
            return new int[]{i + 1, j + 1};
        } else if (sum < target) {
            i++;
        } else {
            j--;
        }
    }
    return null;
}
```



### 220 翻转链表

题意：rt

难度：简单

**方法1**：迭代

```c++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* prev = nullptr;
        ListNode* curr = head;
        while (curr) {
            ListNode* next = curr->next;
            curr->next = prev;
            prev = curr;
            curr = next;
        }
        return prev;
    }
};
```

**方法2**：递归

```c++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if (!head || !head->next) {
            return head;
            //直到当前节点的下一个节点为空时返回当前节点；由于5没有下一个节点了，所以此处返回节点5
        }
        ListNode* newHead = reverseList(head->next);
/*
	第一轮出栈，head为5，head.next为空，返回5
	第二轮出栈，head为4，head.next为5，执行head.next.next=head也就是5.next=4，
把当前节点的子节点的子节点指向当前节点
此时链表为1->2->3->4<->5，由于4与5互相指向，所以此处要断开4.next=null
此时链表为1->2->3->4<-5
返回节点5
	第三轮出栈，head为3，head.next为4，执行head.next.next=head也就是4.next=3，
此时链表为1->2->3<->4<-5，由于3与4互相指向，所以此处要断开3.next=null
此时链表为1->2->3<-4<-5
返回节点5
	第四轮出栈，head为2，head.next为3，执行head.next.next=head也就是3.next=2，
此时链表为1->2<->3<-4<-5，由于2与3互相指向，所以此处要断开2.next=null
此时链表为1->2<-3<-4<-5
返回节点5
	第五轮出栈，head为1，head.next为2，执行head.next.next=head也就是2.next=1，
此时链表为1<->2<-3<-4<-5，由于1与2互相指向，所以此处要断开1.next=null
此时链表为1<-2<-3<-4<-5
返回节点5
出栈完成，最终头节点5->4->3->2->1
*/
        head->next->next = head;
        head->next = nullptr;
        return newHead;
    }
};
```



## 按难度

### 简单

167 两个和 II

#### 最大字串 Maximum SubArray
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
167 两个和 II

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



### 两数之和

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
### 中等

[6 Z字形变换](#6 Z字形变换)

[7 整数反转](# 7 整数反转)

[8 字符串转换整数 (atoi)](# 8 字符串转换整数 (atoi))

[15 三数之和](# 15 三数之和)

[18 四数之和](# 18 四数之和)

#### 55. Jump Game
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
### 困难

[10 正则表达式匹配](# 10 正则表达式匹配)

[32 最长有效括号](# 32 最长有效括号)

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



## 按算法思想

### 双指针

[167 两个和 II](# 167 两个和 II)



### 排序

### 贪心思想

### 二分查找

[34 在排序数组中查找第一个和最后一个位置](# 34 在排序数组中查找第一个和最后一个位置)

### 分治

### 搜索

### 动态规划

### 数学

## 按数据结构

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
