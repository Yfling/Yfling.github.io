



# 📚字符串



## 括号序列（T1）





## 反转字符串（T2）





## 最长回子串（T3）



## 全排列

```js
const permute = (nums) => {
  const res = [];
  const used = {};

  function dfs(path) {
    if (path.length == nums.length) { // 个数选够了
      res.push(path.slice()); // 拷贝一份path，加入解集res
      return;                 // 结束当前递归分支
    }
    for (const num of nums) { // for枚举出每个可选的选项
      // if (path.includes(num)) continue; // 别这么写！查找的时间是O(n)，增加时间复杂度
      if (used[num]) continue; // 使用过的，跳过
      path.push(num);         // 选择当前的数，加入path
      used[num] = true;       // 记录一下 使用了
      dfs(path);              // 基于选了当前的数，递归
      path.pop();             // 上一句的递归结束，回溯，将最后选的数pop出来
      used[num] = false;      // 撤销这个记录
    }
  }

  dfs([]); // 递归的入口，空path传进去
  return res;
};
```





## 判断回文串

```js
function judge (str) {
  const len = str.length
  const mid = parseInt((len - 1) / 2)
  
  for (let i = 0; i <= mid; i++) {
    if (str[i] !== str[len - 1 - i]) {
      return false
    }
  }
  return true
}
```



## 写一个方法找出字符串中出现次数最多的字母（两次）

字典序，最优解是什么

 

## 提取公共字符串

一个面试官考了三道

输入：['aaafsd', 'aawwewer', 'aaddfff']

输出：'aa'





# 📚二叉树



## 

[树的遍历leetcode题目汇总](https://leetcode-cn.com/problems/n-ary-tree-preorder-traversal/solution/yi-tao-quan-fa-shua-diao-nge-bian-li-shu-de-wen--3/)

## 前序遍历

```js
// 前序遍历:
var preOrders = function(root, res = []) {
    if (!root) return res;
    res.push(root.val);
    preOrders(root.left, res)
    preOrders(root.right, res)
    return res;
};
```



## 中序遍历

```js
// 中序遍历:
var inOrders = function(root, res = []) {
    if (!root) return res;
    inOrders(root.left, res);
    res.push(root.val);
    inOrders(root.right, res);
    return res;
};
```

### 

## 后续遍历

```js
// 后序遍历:
var postOrdes = function(root, res = []) {
    if (!root) return res;
    postOrdes(root.left, res);
    postOrdes(root.right, res);
    res.push(root.val);
    return res;
};
```



## 层序遍历

```js
var levelOrder = function(root) {
    const ret = [];
    if (!root) {
        return ret;
    }

    const q = [];
    q.push(root);
    while (q.length !== 0) {
        const currentLevelSize = q.length;
        ret.push([]);
        for (let i = 1; i <= currentLevelSize; ++i) {
            const node = q.shift();
            ret[ret.length - 1].push(node.val);
            if (node.left) q.push(node.left);
            if (node.right) q.push(node.right);
        }
    }
        
    return ret;
};
```







## ？按之字形顺序打印二叉树



## ？蛇形二叉树组合算法



## 求二叉树深度

```js
/* function TreeNode(x) {
    this.val = x;
    this.left = null;
    this.right = null;
} */
function TreeDepth(pRoot)
{
    // write code here
    
    if (pRoot == null) {
        return 0;
    }
    
    var nLeft = TreeDepth(pRoot.left);
    var nRight = TreeDepth(pRoot.right);

    return (nLeft > nRight) ? (nLeft + 1) : (nRight + 1);
}
module.exports = {
    TreeDepth : TreeDepth
};
```





## 两个二叉树节点的第一个公共父节点

```js
/*function ListNode(x) {
	this.val = x;
	this.next = null;
}*/

function FindFirstCommonNode (pHead1, pHead2) {
  let p1 = pHead1;
  let p2 = pHead2;
  
  while(p1 != p2) {
    p1 = p1 ? p1.next : pHead2;
    p2 = p2 ? p2.next : pHead2;
  	return p1;
  }
}
```





## 求根节点到叶节点数字之和

```js
const dfs = (root, prevSum) => {
    if (root === null) {
        return 0;
    }
    const sum = prevSum * 10 + root.val;
    if (root.left == null && root.right == null) {
        return sum;
    } else {
        return dfs(root.left, sum) + dfs(root.right, sum);
    }
}
var sumNumbers = function(root) {
    return dfs(root, 0);
};

```





## 二叉树的之字形层序遍历(NC14) 





# 📚多叉树



## 前序遍历

```js
var preorder = function(root) {
  const res = []
  function traversal (root) {
    if (root !== null) {
      res.push(root.val)
      root.children.forEach(child => traversal(child))
    }
  }
  traversal(root)
  return res
}
```



## 中序遍历





## 后续遍历

```js
var postorder = function(root) {
  const res = []
  function traversal (root) {
    if (root !== null) {
      root.children.forEach(child => {
        traversal(child)
      })
      res.push(root.val)
    }
  }
  traversal(root)
  return res
}
```

 ## 深度遍历

```js
var maxDepth = function(root) {
  if (root === null) {
    return 0
  } else {
    let depth = 1
    function traversal (root, curDepth) {
      if (root !== null) {
        if (curDepth > depth) {
          depth = curDepth
        }
        root.children.forEach(child => traversal(child, curDepth + 1))
      }
    }
    traversal(root, 1)
    return depth
  }
}
```



## 层序遍历





# 📚数组



## 两数之和（TP1）

```js
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



## ？三数之和

其他问法：从数组中找出三数之和为n写在前面 





## 最长无重复子数组（TP2）

```js
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
```





## 合并两个有序的数组（TP3）





## 最大子序列和 

```js
function FindGreatSumOfSubArray(arr) {
  if (arr.length === 0) return 0;
 
  let max = arr[0];
  let temp = arr[0];
 
  for (let i = 0; i < arr.length; i++) {
    temp = temp > 0 ? temp + arr[i] : arr[i];
    max = max > temp ? max : temp
  }
  return max;
}
```



## ？数组中的第K个最大元素



## ？找到出现指定次数的元素



## ？数组顺时针螺旋遍历





# 📚链表



## 反转链表（TP1）



## 排序（TP2）



## 设计LRU缓存结构（TP3）



## 判断单向链表是否有环

```js
/*
 * function ListNode(x) {
 * 		this.val = x;
 *		this.next = null;
 * }
 */

function hasCycle(head) {
  let fast = head;
  let slow = head;
 	while (fast && fast.next) {
    fast = fast.next.next;
    slow = slow.next;
    if (fast === slow) {
      return true;
    }
  }
  return false;
}
```





## 反转链表

```js
// function ListNode(x) {
//     this.val = x;
//     this.next = null;
// } 

function ReverseList(pHead) {
    let pre = null;
    let cur = pHead;
    while (cur !== null) {
        let next = cur.next;
        
        cur.next = pre;
        pre = cur;
        cur = next;
    }
    return pre;
}
```

