# 库函数

- 通常都是左闭右开，例如reverse(s.begin(), s.end())

# 练习

## 344 反转字符串

```c++
class Solution {
public:
    void reverseString(vector<char>& s) {
        int len = s.size();
        for(int i = 0, j = len - 1; i < len / 2; i++, j--){
            swap(s[i],s[j]);
        }
    }
};
```

