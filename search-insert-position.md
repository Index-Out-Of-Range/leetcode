# Search Insert Position

## 有序数组查找元素使用二分法

## C++

```text
class Solution
{
  public:
    int searchInsert(vector<int> &nums, int target)
    {
        if(target<nums[0])
            return 0;
        int n = nums.size();
        for (int i = 0; i < n; i++)
        {
            if (target == nums[i])
                return i;
            if (nums[i] < target && (i+1<n && target < nums[i + 1]))
                return i+1;
        }
        return n;
    }
};
```

### 使用二分法

```text
class Solution
{
  public:
    int searchInsert(vector<int> &nums, int target)
    {
        int low = 0, high = nums.size() - 1;
        while (low <= high)
        {
            int mid = low + (high - low) / 2;
            if (nums[mid] < target)
                low = mid + 1;
            else
            {
                high = mid - 1;
            }
        }
        return low;
    }
};
```

## python

```text
class Solution:
    def searchInsert(self, nums: 'List[int]', target: 'int') -> 'int':
        return sorted(nums+[target]).index[target]
```

