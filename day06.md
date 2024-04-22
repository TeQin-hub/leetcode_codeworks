# 哈希

当需要在“一个范围内，判断是否一个元素出现过”

## 数据结构

### 数组

### set

### map

# 练习

## 242 有效字母异位

```c++
class Solution {
public:
    bool isAnagram(string s, string t) {
        int hashTable[26]={0};
        for(int i = 0; i < s.size(); i++){
            hashTable[s[i] - 'a']++;
        }
        for(int j = 0; j < t.size(); j++){
            hashTable[t[j] - 'a']--;
        }
        for(int k = 0; k < 26; k++){
            if(hashTable[k] != 0){
                return false;
            }
        }
        return true;
    }
};
```

## 349 两个数组的交集

```c++
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        // set哈希
        unordered_set<int> hashTable;
        unordered_set<int> result;
        for(int i = 0; i < nums1.size(); i++){
            hashTable.insert(nums1[i]);
        } 
        for(int j =0; j < nums2.size(); j++){
            if(hashTable.find(nums2[j]) != hashTable.end()){
                result.insert(nums2[j]);
            }
        }
        return vector(result.begin(),result.end());
    }
};
```

```c++
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        // 因为限制了数组包含的数字的大小<=1000，所以可以使用数组且效率更高
        int hashTable[1005] = {0};
        unordered_set<int> result;
        for(int i = 0; i < nums1.size(); i++){
            hashTable[nums1[i]] = 1;
        }
        for(int j= 0; j < nums2.size(); j++){
            if(hashTable[nums2[j]] == 1){
                result.insert(nums2[j]);
            }
        }
        return vector(result.begin(),result.end());
    }
};
```

## 202 快乐数

构造函数sumSqual，简化逻辑

```c++
class Solution {
public:
    int sumSqual(int n){
        int sum = 0;
        while(n){
            int d = 0;
            d = n % 10;
            sum += d * d;
            n /= 10;
        }
        return sum;
    }
    bool isHappy(int n) {
        unordered_set<int> hashTable;
        int sum = n;
        while(1){
            sum = sumSqual(sum);
            if(sum == 1){
                return true;
            }
            if(hashTable.find(sum) != hashTable.end()){
                return false;
            }
            hashTable.insert(sum);
        }
    }
};
```

## 1 两数之和

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> hashTable;
        for(int i = 0; i < nums.size(); i++){
            int s = target - nums[i];
            auto iter = hashTable.find(s);
            if(iter != hashTable.end()){
                return {iter->second,i};
            }
            hashTable.insert(pair<int,int>(nums[i],i));
        }
        return vector<int>{};
    }
};
```

