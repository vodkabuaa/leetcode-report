
#题目
###Given an unsorted integer array, find the first missing positive integer.

###For example,
###Given [1,2,0] return 3,and [3,4,-1,1] return 2.

###Your algorithm should run in O(n) time and uses constant space.


class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        if (nums.size() == 0){
            return 1;
        }
        
        int nums_max = -100000;
        int nums_min = 1000000;
        unordered_map<int,int> hashtable;
        for (int i = 0; i < nums.size(); ++i){
            nums_max = max(nums_max,nums[i]);
            nums_min = min(nums_min,nums[i]);
            hashtable.insert({nums[i], i});
        }
        
        if (nums_min > 1 ){
            return 1;
        }
        
        for (int i = nums_min ; i <= nums_max; ++i){
            if(i > 0 && hashtable.count(i) == 0){
                return i;
            }
        }
        return nums_max + 1;
        
    }
};

#分析
###本题的难点是在于对多种情况的讨论分析，在完成代码前一定要把多种边界条件考虑清楚。由于这题是确实的最小整数。所以先找到array的最大值以及最小值
###然后分三种情况讨论，第一种是最小值本身就大于1,那么确实的最小正整数肯定是1，然后如果最小值是负数，则需要对中间的情况进行检查。
