# 练习

## 20 有效括号

注意 思路：消除 使用栈很合适

```c++
class Solution {
public:
    bool isValid(string s) {
        stack<int> st;
        for(int i = 0; i < s.size(); i++){
            if(s[i] == '(') st.push(')');
            else if(s[i] == '{') st.push('}');
            else if(s[i] == '[') st.push(']');
            // 注意这里条件是 ||
            else if(st.empty() || st.top() != s[i]) return false;
            else st.pop();
        }
        return st.empty();
    }
};
```

## 1047 删除字符串中的所有相邻重复项

- 要记录上一个遍历的元素是什么，需要一个结构帮助我们记录一下，使用栈很合适
- 也可以用一个字符串来模拟这个栈的行为，因为最后输出也是一个字符串

```c++
class Solution {
public:
    // 库函数的使用
    string removeDuplicates(string s) {
        string result;
        for(int i = 0; i < s.size(); i++){
            if(!result.empty() && s[i] == result.back()) result.pop_back();
            else result.push_back(s[i]);
        }
        return result;
    }
};
```

## 150 逆波兰表达式求值

栈记录数字值，遇到符号，则弹出（消除）两个数字

```c++
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        stack<long long> st;
        for(int i = 0; i < tokens.size(); i++){
            // 注意除号 /
            if(tokens[i] == "+" || tokens[i] == "*" || tokens[i] == "-" || tokens[i] == "/"){
                long long num1 = st.top();
                st.pop();
                long long num2 = st.top();
                st.pop();
                if(tokens[i] == "+") st.push(num1 + num2);
                else if(tokens[i] == "*") st.push(num1 * num2);
                else if(tokens[i] == "-") st.push(num2 - num1);
                else st.push(num2 / num1);
            }else{
                st.push(stoll(tokens[i]));
            }
        }
        long long result = st.top();
        // 回收内存
        st.pop();
        return result;
    }
};
```



# 感想

栈结构很适合消除两两相邻的字符（数字）