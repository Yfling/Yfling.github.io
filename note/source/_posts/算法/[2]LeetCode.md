https://leetcode-cn.com/company/bytedance/problemset/

[🔥 LeetCode 热题 HOT 100](https://leetcode-cn.com/problem-list/2cktkvj)

[字节题](https://leetcode-cn.com/company/bytedance/problemset/)



做题顺序：高频 -> 低频



js算法：不能用任何语法糖，比如arr.sort()



# [1. 两数之和](https://leetcode-cn.com/problems/two-sum/)👌

难度：简单

>  给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 target  的那 两个 整数，并返回它们的数组下标。
>
> 你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。
>
> 你可以按任意顺序返回答案。



>输入：nums = [2,7,11,15], target = 9
>输出：[0,1]
>解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。



```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */

 var twoSum = function(nums, target) {
    let map = new Map();
    for(let i = 0; i < nums.length; i++){
        if (map.has(target - nums[i])){
            return [map.get(target - nums[i]), i];
        } else {
            map.set(nums[i], i);
        }
    }
    return [];
};

// 
const nums = [2,7,11,15];
const target = 9;
console.log(twoSum(nums, target))
```





# [2. 两数相加](https://leetcode-cn.com/problems/add-two-numbers/)👌

难度：中等

>给你两个**非空**的链表，表示两个非负的整数。它们每位数字都是按照**逆序**的方式存储的，并且每个节点只能存储 一位 数字。
>
>请你将两个数相加，并以相同形式返回一个表示和的链表。
>
>你可以假设除了数字 0 之外，这两个数都不会以 0 开头

```
输入：l1 = [2,4,3], l2 = [5,6,4]
输出：[7,0,8]
解释：342 + 465 = 807.
```

```javascript
var addTwoNumbers = function(l1, l2) {
    let head = null, tail = null;
    let carry = 0;
    while (l1 || l2) {
        const n1 = l1 ? l1.val : 0;
        const n2 = l2 ? l2.val : 0;
        const sum = n1 + n2 + carry;
        if (!head) {
            head = tail = new ListNode(sum % 10);
        } else {
            tail.next = new ListNode(sum % 10);
            tail = tail.next;
        }
        carry = Math.floor(sum / 10);
        if (l1) {
            l1 = l1.next;
        }
        if (l2) {
            l2 = l2.next;
        }
    }
    if (carry > 0) {
        tail.next = new ListNode(carry);
    }
    return head;
};
```





# [3. 无重复字符的最长子串](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)👌

难度：中等 `滑动窗口`

> 题目：给定一个字符串 `s` ，请你找出其中不含有重复字符的 **最长子串** 的长度。



```示例：
输入: s = "abcabcbb"
输出: 3 

输入: s = "bbbbb"
输出: 1

输入: s = "pwwkew"
输出: 3

输入: s = ""
输出: 0
```

```javascript
// 考点：双指针、滑动窗口
const str = 'abcabcbb';
var lengthOfLongestSubstring = function(s) {
    const occ = new Set();  // 哈希集合，记录每个字符是否出现过
    const n = s.length;  // 右指针，初始值为 -1，相当于我们在字符串的左边界的左侧，还没有开始移动
    let rk = -1, ans = 0;
    for (let i = 0; i < n; ++i) {
        if (i != 0) {
            occ.delete(s.charAt(i - 1));  // 左指针向右移动一格，移除一个字符
        }
        while (rk + 1 < n && !occ.has(s.charAt(rk + 1))) {  // set中没有该字符，移动右指针
            occ.add(s.charAt(rk + 1));
            ++rk;
        }
        ans = Math.max(ans, rk - i + 1);  // 第 i 到 rk 个字符是一个极长的无重复字符子串
    }
    return ans;
};
lengthOfLongestSubstring(str)

// charAt() 方法从一个字符串中返回指定的字符。
// 用法: str.charAt(index)


// console
const str = 'abcabcbb';
let lengthOfLongestSubstring = function(s) {
 console.log('----------------------------------------------------------------------')
 const occ = new Set();  // 哈希集合，记录每个字符是否出现过
 const n = s.length;  // 右指针，初始值为 -1，相当于我们在字符串的左边界的左侧，还没有开始移动
 let rk = -1, ans = 0;
 for (let i = 0; i < n; ++i) {
  console.log('------------------------')
  if (i !== 0) {
   occ.delete(s.charAt(i - 1));  // 左指针向右移动一格，移除一个字符
  }
  while (rk + 1 < n && !occ.has(s.charAt(rk + 1))) {  // set中没有该字符，移动右指针
   occ.add(s.charAt(rk + 1));
   ++rk;
  }
  ans = Math.max(ans, rk - i + 1);  // ans保留的是历史ans最大值
  console.log(`i: ${i}, rk: ${rk}, ans: ${ans}`);
  console.log(occ)
 }
 return ans;
};
lengthOfLongestSubstring(str)

// charAt() 方法从一个字符串中返回指定的字符。
// 用法: str.charAt(index)
```

[视频解释](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/solution/wu-zhong-fu-zi-fu-de-zui-chang-zi-chuan-by-leetc-2/)

边界情况：

- 字符串为空
- 字符串全部重复

总结：

- 涉及到子串，一般要用散列表

  

# [4. 寻找两个正序数组的中位数](https://leetcode-cn.com/problems/median-of-two-sorted-arrays/)👌

给定两个大小分别为 `m` 和 `n` 的正序（从小到大）数组 `nums1` 和 `nums2`。请你找出并返回这两个正序数组的 **中位数** 。

```
输入：nums1 = [1,3], nums2 = [2]
输出：2.00000
解释：合并数组 = [1,2,3] ，中位数 2
```

```js
/**
 *
 *
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number}
 */
let findMedianSortedArrays = function (nums1, nums2) {
    let n1 = nums1.length;
    let n2 = nums2.length;

    // 两个数组总长度
    let len = n1 + n2;

    // 保存当前移动的指针的值(在nums1或nums2移动)，和上一个值
    let preValue = -1;
    let curValue = -1;

    //  两个指针分别在nums1和nums2上移动
    let point1 = 0;
    let point2 = 0;

    // 需要遍历len/2次，当len是奇数时，最后取curValue的值，是偶数时，最后取(preValue + curValue)/2的值
    for (let i = 0; i <= Math.floor(len / 2); i++) {
        preValue = curValue;
        // 这句话没太懂：需要在nums1上移动point1指针
        if (point1 < n1 && (point2 >= n2 || nums1[point1] < nums2[point2])) {
            curValue = nums1[point1];
            point1++;
        } else {
            curValue = nums2[point2];
            point2++;
        }
    }

    return len % 2 === 0
        ? (preValue + curValue) / 2
        : curValue
};

```



# [5. 最长回文子串](https://leetcode-cn.com/problems/longest-palindromic-substring/)(没看懂)👌

https://leetcode-cn.com/problems/longest-palindromic-substring/solution/chao-jian-dan-de-zhong-xin-kuo-san-fa-yi-qini/

```js
/**
 * @param {string} s
 * @return {string}
 */
var longestPalindrome = function(s) {
        if (s.length<2){
            return s
        }
        let res = ''
        for (let i = 0; i < s.length; i++) {
            // 回文子串长度是奇数
            helper(i, i)
            // 回文子串长度是偶数
            helper(i, i + 1) 
        }

        function helper(m, n) {
            while (m >= 0 && n < s.length && s[m] == s[n]) {
                m--
                n++
            }
            // 注意此处m,n的值循环完后  是恰好不满足循环条件的时刻
            // 此时m到n的距离为n-m+1，但是mn两个边界不能取 所以应该取m+1到n-1的区间  长度是n-m-1
            if (n - m - 1 > res.length) {
                // slice也要取[m+1,n-1]这个区间 
                res = s.slice(m + 1, n)
            }
        }
        return res
};

```





# [15. 三数之和](https://leetcode-cn.com/problems/3sum/)👌

中等

[图解](https://leetcode-cn.com/problems/3sum/solution/hua-jie-suan-fa-15-san-shu-zhi-he-by-guanpengchn/)



```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var threeSum = function(nums) {
    let ans = [];
    const len = nums.length;
    if(nums == null || len < 3) return ans;
    nums.sort((a, b) => a - b); // 排序
    for (let i = 0; i < len ; i++) {
        if(nums[i] > 0) break; // 如果当前数字大于0，则三数之和一定大于0，所以结束循环
        if(i > 0 && nums[i] == nums[i-1]) continue; // 去重
        let L = i+1;
        let R = len-1;
        while(L < R){
            const sum = nums[i] + nums[L] + nums[R];
            if(sum == 0){
                ans.push([nums[i],nums[L],nums[R]]);
                while (L<R && nums[L] == nums[L+1]) L++; // 去重
                while (L<R && nums[R] == nums[R-1]) R--; // 去重
                L++;
                R--;
            }
            else if (sum < 0) L++;
            else if (sum > 0) R--;
        }
    }        
    return ans;
};
```







# [20. 有效的括号](https://leetcode-cn.com/problems/valid-parentheses/)







视频课程：

1. [JavaScript版数据结构与算法 轻松解决前端算法面试](https://coding.imooc.com/class/chapter/446.html#Anchor)
2. [算法与数据结构体系课](https://class.imooc.com/sale/datastructure?mc_marking=847f8fb5de6faa3343df639065d45b7d&mc_channel=imoocsearch)



