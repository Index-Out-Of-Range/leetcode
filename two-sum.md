# **关键在于只写一层循环，降低时间复杂度**

## C++
### 使用unordered_map
### find函数。
`iterator find ( const key_type& key );`
如果key存在，则find返回key对应的迭代器，如果key不存在，则find返回unordered_map::end。因此可以通过

`map.find(key) == map.end()`
来判断，key是否存在于当前的unordered_map中。



```
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