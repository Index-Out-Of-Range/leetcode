## C++


```

#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

class Solution
{
  public:
    int maxSubArray(vector<int> &nums)
    {
        int ans = nums[0], sum = 0;
        for (int i = 0; i < nums.size(); i++)
        {
            sum += nums[i];
            ans = max(sum, ans);
            sum = max(sum, 0);
        }
        return ans;
    }
};
```

### divide and conquer（不是很懂）
* Divide-and-Conquer算法将nums分成两半，并递归地找到它们中的最大子阵列和。 嗯，最棘手的部分是处理最大子阵列跨越两半的情况。 对于这种情况，我们使用线性算法：从中间元素开始并移动到两端（左端和右端），记录我们看到的最大总和。 在这种情况下，最大总和最终等于中间元素加上向左移动的最大总和和向右移动的最大总和。



```
class Solution
{
  public:
    int maxSubArray(vector<int> &nums)
    {
        return maxSub(nums, 0, nums.size() - 1);
    }

  private:
    int maxSub(vector<int> &nums, int left, int right)
    {
        if (left > right)
            return INT_MIN;
        int middle = left + (right - 1) / 2;
        int left_max = maxSub(nums, left, middle - 1);
        int right_max = maxSub(nums, middle + 1, right);
        int ml = 0, mr = 0;
        for (int i = middle - 1, sum = 0; i >= left; i--)
        {
            sum += nums[i];
            ml = max(ml, sum);
        }
        for (int i = middle + 1, sum = 0; i <= right; i++)
        {
            sum += nums[i];
            mr = max(mr, sum);
        }
        return max(max(left_max, right_max), ml + mr + nums[middle]);
    }
};
```

## python


```

class Solution:
    def maxSubArray(self, A):
        if not A:
            return 0
        cur_sum = max_sum = A[0]
        for num in A[1:]:
            cur_sum = max(num, cur_sum+num)
            max_sum = max(max_sum, cur_sum)
        return max_sum
        
```


