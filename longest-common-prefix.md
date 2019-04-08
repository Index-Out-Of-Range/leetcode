# Longest Common Prefix

## C++

```text
#include <iostream>
#include <vector>
#include <string>
using namespace std;

class Solution
{
  public:
    string longestCommonPrefix(vector<string> &strs)
    {
        if (strs.size() == 0)
            return "";
        string result = strs[0];
        for (int i = 0; i < strs[0].length(); i++)
        {
            for (int j = 1; j < strs.size(); j++)
            {
                if (i == strs[j].length() || strs[j][i] != strs[0][i])
                    return strs[0].substr(0, i);
            }
        }
        return strs[0];
    }
};

int main()
{
    Solution *s = new Solution();
    vector<string> vec;
    vec.push_back("leetcode");
    vec.push_back("leedcode");
    vec.push_back("leetcodes");
    cout << s->longestCommonPrefix(vec) << endl;
    system("pause");
    return 0;
}
```

## Java

Sort the array first, and then you can simply compare the first and last elements in the sorted array.

```text
public String longestCommonPrefix(String[] strs) {
        StringBuilder result = new StringBuilder();

        if (strs!= null && strs.length > 0){

            Arrays.sort(strs);

            char [] a = strs[0].toCharArray();
            char [] b = strs[strs.length-1].toCharArray();

            for (int i = 0; i < a.length; i ++){
                if (b.length > i && b[i] == a[i]){
                    result.append(b[i]);
                }
                else {
                    return result.toString();
                }
            }
        return result.toString();
    }
```

## python

```text
class Solution:
    def longestCommonPrefix(self, strs):
        """
        :type strs: List[str]
        :rtype: str
        """
        if not strs:
            return ""
        s1 = min(strs)
        s2 = max(strs)
        for i, ch in enumerate(s1):
            if ch != s2[i]:
                return s1[:i]
        return s1
```

