# Two Sum

## C++

### 使用unordered\_map

### find函数。

`iterator find ( const key_type& key );` 如果key存在，则find返回key对应的迭代器，如果key不存在，则find返回unordered\_map::end。因此可以通过

`map.find(key) == map.end()` 来判断，key是否存在于当前的unordered\_map中。

```text
#include <iostream>
#include <unordered_map>
using namespace std;

class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> hash;
        vector<int> result;
        for (int i = 0; i < nums.size(); i++) {
            int numberToFind = target - nums[i];
            if (hash.find(numberToFind) != hash.end()) {
                cout << "Solution " << i << endl;
                result.push_back(hash[numberToFind]);
                result.push_back(i);
                return result;
            }
            hash[nums[i]] = i;
            cout << i << endl;
            for (auto iter = hash.begin(); iter != hash.end(); iter++) {
                cout << iter->first << "\t" << iter->second << endl;
            }
        }
        return result;
    }
};

int main()
{
    Solution *s = new Solution();
    vector<int> nums = { 2,11,15,7 };
    vector<int> result = s->twoSum(nums, 9);
    for (int i = 0; i < result.size(); i++)
        cout << result[i] << endl;
    system("pause");
    return 0;
}
```

## Java

## Python

```text
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        if len(nums)<0:
            return None
        buffer_dict = {}
        for i in range(len(nums)):
            if nums[i] in buffer_dict:
                return [buffer_dict[nums[i]], i]
            else:
                buffer_dict[target-nums[i]] = i
```

