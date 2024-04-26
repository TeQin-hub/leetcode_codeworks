# 练习

## 232 用栈实现队列

```c++
class MyQueue {
public:
    stack<int> sIn;
    stack<int> sOut;
    MyQueue() {

    }
    
    void push(int x) {
        sIn.push(x);
    }
    
    int pop() {
        //注意要先判sOut为空，才将sIn的所有内容传入sOut
        if(sOut.empty()){
            while(!sIn.empty()){
                sOut.push(sIn.top());
                sIn.pop();
            }
        }
        int x = sOut.top();
        sOut.pop();
        return x;
    }
    
    int peek() {
        // 注意调用类的成员函数  使用this
        int x = this->pop();
        // 注意是sOut
        sOut.push(x);
        return x;
    }
    
    bool empty() {
        return (sIn.empty() && sOut.empty());
    }
};

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue* obj = new MyQueue();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->peek();
 * bool param_4 = obj->empty();
 */
```

## 225 用队列实现栈

```c++
class MyStack {
public:
    queue<int> st;
    MyStack() {

    }
    
    void push(int x) {
        st.push(x);
    }
    
    int pop() {
        int size = st.size();
        size--;
        while(size--){
            // 注意 queue容器适配器使用的front
            st.push(st.front());
            st.pop();
        }
        int x = st.front();
        st.pop();
        return x;
    }
    
    int top() {
        return st.back();
    }
    
    bool empty() {
        return st.empty();
    }
};

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack* obj = new MyStack();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->top();
 * bool param_4 = obj->empty();
 */
```

# 感想

学习使用栈和队列，不会的函数，懂得查手册