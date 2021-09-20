

[🔥 LeetCode 热题 HOT 100](https://leetcode-cn.com/problem-list/2cktkvj)



做题顺序：高频 -> 低频





# [1. 两数之和](https://leetcode-cn.com/problems/two-sum/)

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



# [15. 三数之和](https://leetcode-cn.com/problems/3sum/)





# [2. 两数相加](https://leetcode-cn.com/problems/add-two-numbers/)

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





# [3. 无重复字符的最长子串](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)

难度：中等

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
        while (rk + 1 < n && !occ.has(s.charAt(rk + 1))) {  // 只要set中没有出现重复的字符，就不断地移动右指针
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
```



# [5. 最长回文子串](https://leetcode-cn.com/problems/longest-palindromic-substring/)









# [20. 有效的括号](https://leetcode-cn.com/problems/valid-parentheses/)







视频课程：

1. [JavaScript版数据结构与算法 轻松解决前端算法面试](https://coding.imooc.com/class/chapter/446.html#Anchor)
2. [算法与数据结构体系课](https://class.imooc.com/sale/datastructure?mc_marking=847f8fb5de6faa3343df639065d45b7d&mc_channel=imoocsearch)



