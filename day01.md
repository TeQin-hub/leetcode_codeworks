# 二分法

## 左闭右闭

```c++
left = 0;
right = numsize - 1;
while(left <= right){
// 在左闭右闭的区间，= 是合法的，所以要有等号
    middle = (right - left) / 2 + left;
    if(nums[middle] > target){
  		//因为是右闭，所以已经确定了当前下标nums[middle]已经是>target了，
        //所以这个middle可以不放入下一个搜索空间
        right = middle - 1;
    }else if(nums[middle] < target){
        //同理
        left = middle + 1;
    }else {
        return middle;
    }
    return -1;
}

```

## 左闭右开

```c++
left = 0;
right = numsize;
while(left < right){
    middle = (right - left) / 2 + left;
    if(nums[middle] > target){
        right = middle;
    }else if(nums[middle] < target){
        left = middle + 1;
    }else{
        return middle;
    }
    return -1;
}
```

> 综上所述，当nums[middle]大于或者小于target时，这个nums[middle]都不需要放入下一次的搜索空间了，所以都需要将这个nums[middle]去掉，只是在开闭区间的不同条件下，right和left的更新等式是不同的

# 移除元素

## 双指针

- **一个指针read来读数，判断是否符合条件，符合条件的数则赋值给write指针**
- 将两层for循环可以变为一个for循环

```c++
int fast = 0;
int slow = 0;
for(;fast < nums.size();fast++){
    if(nums[fast] != target){
        nums[slow++] = nums[fast];
    }
}
```

# 练习

## 704 二分查找

```c++
class Solution {
public:
    int search(vector<int>& nums, int target) {
        //左闭右闭
        int left = 0;
        int right = nums.size() - 1;
        while(left <= right){
            int mid = (right - left) / 2 + left;
            if(nums[mid] > target){
                right = mid -1;
            }else if(nums[mid] < target){
                left = mid + 1;
            }else{
                return mid;
            }
        }
        return -1;
    }
};
```

## 27 移除元素

```c++
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int fast = 0, slow = 0;
        for(; fast < nums.size(); fast++){
            if(nums[fast] != val){
                nums[slow++] = nums[fast];
            }
        }
        return slow;
    }
};
```

# 感想

读研后，自己有做mit s6081的操作系统的项目，是使用c代码写的，不过题解都是在网上看答案，然后只是自己理解。对于算法题一直没有机会练习，然后也可能今天是第一天题目并没有特别难，看完学习视频后，都能很快的写出来，坚持！！！