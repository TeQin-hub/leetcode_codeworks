# 库函数

- 通常都是左闭右开，例如reverse(s.begin(), s.end())

# 数组扩充

从前向后填充就是O(n^2)的算法了，因为每次添加元素都要将添加元素之后的所有元素整体向后移动。

**其实很多数组填充类的问题，其做法都是先预先给数组扩容带填充后的大小，然后在从后向前进行操作。**

这么做有两个好处：

1. 不用申请新数组。
2. 从后向前填充元素，避免了从前向后填充元素时，每次添加元素都要将添加元素之后的所有元素向后移动的问题。

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

## 541 反转字符串

注意 库函数的参数

```c++
class Solution {
public:
    string reverseStr(string s, int k) {
        for(int i = 0; i < s.size(); i += 2*k){
            //  注意该if条件中 有等号
            if(i + k <= s.size()){
                // 注意reverse 左闭右开 [i,i+k)
                reverse(s.begin() + i,s.begin() + i + k);
                continue;
            }
            reverse(s.begin() + i,s.end());
        }
        return s;
    }
};
```

## 卡 54 替换数字

**双指针法**

```c++
#include <iostream>
using namespace std;

int main(){
    string s;
    while(cin >> s){
        int oldIndex = s.size() - 1;
        int count = 0;
        for(int i = 0; i < s.size(); i++){
            if(s[i] >= '0' && s[i] <= '9'){
                count++;
            }
        }
        
        // 扩充数组
        s.resize(s.size() + 5 * count);
        int newIndex = s.size() - 1;
        
        // 从后往前进行填充
        while(oldIndex >= 0){
            if(s[oldIndex] >= '0' && s[oldIndex] <= '9'){
                s[newIndex--] = 'r';
                s[newIndex--] = 'e';
                s[newIndex--] = 'b';
                s[newIndex--] = 'm';
                s[newIndex--] = 'u';
                s[newIndex--] = 'n';
            }else{
                s[newIndex--] = s[oldIndex];
            }
            oldIndex--;
        }
        cout << s << endl;
       
    }
    return 0;
}
```

## 151 反转字符串中的单词 

```c++
class Solution {
public:
    // 反转单词
    void reverseStr(string &s, int start, int end){
        // 注意这里 start != end 会报错，想想字符串偶数的情况
        for(; start < end; start++,end--){
            swap(s[start],s[end]);
        }
    }
    // 删去空格
    void deleteSpace(string &s){
        // 双指针
        int slow = 0, fast = 0;
        for(;fast < s.size(); fast++){
            if(s[fast] != ' '){
                if(slow != 0) s[slow++] = ' ';
                while(fast < s.size() && s[fast] != ' '){
                    s[slow++] = s[fast++];
                }
            }
        }
        s.resize(slow);
    }
    string reverseWords(string s) {
        deleteSpace(s);
        reverseStr(s,0,s.size()-1);
        int start = 0;
        for(int i = 0; i <= s.size(); i++){
            if(s[i] == ' ' || i == s.size()){
                reverseStr(s,start,i-1);
                start = i + 1;
            }
        }
        return s;
    }
};
```

## k55 右旋字符串

```c++
#include <iostream>
#include <algorithm>
using namespace std;

int main(){
    int k;
    string s;
    cin >> k >> s;
    // 先整体逆转，在局部逆转
    reverse(s.begin(),s.end());
    reverse(s.begin(), s.begin() + k);
    reverse(s.begin() + k,s.end());
    cout << s;
    return 0;
}
```

# 感想

- 替换数字，学会数组扩充方法：先扩大数组，然后从后往前来写，其中oldIndex（read）、newIndex（write)
- 反转字符串中的单词：整体反转+局部反转