# Marcos-cc.github.io

## 二分查找
二分最关键的在于确定区间划分的形式，是要用[l, r]还是[l, R) 
一旦确定形式，在查找过程中就不改变了。
具体逻辑(l, r 是怎么变)想想就不会错了
```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        // [l, r]
        /*int l = 0, r = nums.size() - 1;
        while(l <= r) {
            int mid = l + (r - l)/2;
            int x = nums[mid];
            if(x < target) {
                l = mid + 1;
            }
            else if(x == target) {
                return mid;
            }
            else {
                r = mid - 1;
            }
        }
        return -1;
        */
        // [l, r)
        int l = 0, r = nums.size();
        while(l < r) {
            int mid = l + (r - l)/2;
            int x = nums[mid];
            if(target < x) {
                r = mid;
            }
            else if(target == x){
                return mid;
            }
            else {
                l = mid + 1;
            }
        }
        return -1;
    }
};
```

## 移除元素 
空间复杂度O(n)的方法就不说了，这里看看O(1)是如何实现的，我们不妨逆向思维，删去==val的值也就是保留!=val的值，因此只要把!=val的值依次保留即可，这里需要思考的是，如何保留？
也就放哪里，怎么放的问题，我们需要保证的是已经遍历的数字和存放位置不会对将来的判断造成影响，所以我们放的位置应该是已经遍历过的位置，不妨从左往右遍历，那么放的位置就是从0->n-1
使用idx=0开始表示存放下标，从左往右遍历，一旦遇到`nums[i]!=val`就放到`nums[idx++]`的位置。
数组的长度也就是idx的大小

代码：
```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int idx = 0;
        for(int i = 0; i < nums.size(); ++i) {
            if(nums[i] != val) {
                nums[idx++] = nums[i];
            }
        }
        nums.resize(idx);
        return idx;
    }
};
```