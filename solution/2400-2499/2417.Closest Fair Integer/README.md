# [2417. Closest Fair Integer](https://leetcode.cn/problems/closest-fair-integer)

[English Version](/solution/2400-2499/2417.Closest%20Fair%20Integer/README_EN.md)

## 题目描述

<!-- 这里写题目描述 -->

<p>You are given a <strong>positive</strong> integer <code>n</code>.</p>

<p>We call an integer <code>k</code> fair if the number of <strong>even</strong> digits in <code>k</code> is equal to the number of <strong>odd</strong> digits in it.</p>

<p>Return <em>the <strong>smallest</strong> fair integer that is <strong>greater than or equal</strong> to </em><code>n</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> n = 2
<strong>Output:</strong> 10
<strong>Explanation:</strong> The smallest fair integer that is greater than or equal to 2 is 10.
10 is fair because it has an equal number of even and odd digits (one odd digit and one even digit).</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> n = 403
<strong>Output:</strong> 1001
<strong>Explanation:</strong> The smallest fair integer that is greater than or equal to 403 is 1001.
1001 is fair because it has an equal number of even and odd digits (two odd digits and two even digits).
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 10<sup>9</sup></code></li>
</ul>

## 解法

<!-- 这里可写通用的实现逻辑 -->

**方法一：分类讨论**

我们记 $n$ 的位数为 $k$，奇数位数、偶数位数分别为 $a$ 和 $b$。

-   若 $a=b$，则 $n$ 本身就是 `fair` 的，直接返回 $n$ 即可；
-   否则，若 $k$ 为奇数，那么我们找到 $k+1$ 位的最小 `fair` 数即可，形如 `10000111`；若 $k$ 为偶数，我们直接暴力递归 `closestFair(n+1)` 即可。

时间复杂度 $O(\sqrt{n} \times \log_{10} n)$。

<!-- tabs:start -->

### **Python3**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```python
class Solution:
    def closestFair(self, n: int) -> int:
        a = b = k = 0
        t = n
        while t:
            if (t % 10) & 1:
                a += 1
            else:
                b += 1
            t //= 10
            k += 1
        if k & 1:
            x = 10**k
            y = int('1' * (k >> 1) or '0')
            return x + y
        if a == b:
            return n
        return self.closestFair(n + 1)
```

### **Java**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```java
class Solution {
    public int closestFair(int n) {
        int a = 0, b = 0;
        int k = 0, t = n;
        while (t > 0) {
            if ((t % 10) % 2 == 1) {
                ++a;
            } else {
                ++b;
            }
            t /= 10;
            ++k;
        }
        if (k % 2 == 1) {
            int x = (int) Math.pow(10, k);
            int y = 0;
            for (int i = 0; i < k >> 1; ++i) {
                y = y * 10 + 1;
            }
            return x + y;
        }
        if (a == b) {
            return n;
        }
        return closestFair(n + 1);
    }
}
```

### **C++**

```cpp
class Solution {
public:
    int closestFair(int n) {
        int a = 0, b = 0;
        int t = n, k = 0;
        while (t) {
            if ((t % 10) & 1) {
                ++a;
            } else {
                ++b;
            }
            ++k;
            t /= 10;
        }
        if (a == b) {
            return n;
        }
        if (k % 2 == 1) {
            int x = pow(10, k);
            int y = 0;
            for (int i = 0; i < k >> 1; ++i) {
                y = y * 10 + 1;
            }
            return x + y;
        }
        return closestFair(n + 1);
    }
};
```

### **Go**

```go
func closestFair(n int) int {
	a, b := 0, 0
	t, k := n, 0
	for t > 0 {
		if (t%10)%2 == 1 {
			a++
		} else {
			b++
		}
		k++
		t /= 10
	}
	if a == b {
		return n
	}
	if k%2 == 1 {
		x := int(math.Pow(10, float64(k)))
		y := 0
		for i := 0; i < k>>1; i++ {
			y = y*10 + 1
		}
		return x + y
	}
	return closestFair(n + 1)
}
```

### **TypeScript**

```ts

```

### **...**

```

```

<!-- tabs:end -->