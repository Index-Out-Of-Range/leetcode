## C++

### 使用两个指针


```

class Solution
{
  public:
    int removeElement(vector<int> &nums, int val)
    {
        int i = 0;
        for (int j = 0; j < nums.size(); j++)
        {
            if (nums[j] != val)
            {
                nums[i] = nums[j];
                i++;
            }
        }
        return i;
    }
};
```

### 如果遇到val将它和数组最后一个数交换，减少交换次数


```

class Solution
{
  public:
    int removeElement(vector<int> &nums, int val)
    {
        int i = 0;
        int n = nums.size();
        while (i < n)
        {
            if (nums[i] == val)
            {
                nums[i] = nums[n - 1];
                n--;
            }
            else
            {
                i++;
            }
        }
        return n;
    }
};
```

