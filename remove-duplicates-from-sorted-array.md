## C++

### vector从第一个元素开始遍历
    

```
    for (vector<int>::iterator it = nums.begin() + 1; it != nums.end();)
    {
        
    }
```


```

class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if(nums.empty()) return 0;
        int i=0,j=1;
        for(;j<nums.size();j++)
        {
            if(nums[i]!=nums[j])
            {
                i++;
                nums[i] = nums[j];
            }
        }
        return i+1;
    }
};
```

## python
### OrderedDict的键值是有序的

```

from collections import OrderedDict

class Solution:
    def removeDuplicates(self, nums: 'List[int]') -> 'int':
        nums[:] = OrderedDict.fromkeys(nums).keys()
        return len(nums)
```

