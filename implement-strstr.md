## C++

```
class Solution
{
  public:
    int strStr(string haystack, string needle)
    {
        if (needle.size() == 0)
            return 0;
        string::size_type position = haystack.find(needle);
        if (position != haystack.npos)
        {
            cout << "position is: " << position << endl;
            return position;
        }
        else
        {
            cout << "Not found." << endl;
            return -1;
        }
    }
};
```



### Brute-Force

* Traverse all the possible starting points of `haystack` (from `0` to `haystack.length() - needle.length()` ) and see if the following characters in `haystack` match those of `needle`。



```

class Solution {
public:
    int strStr(string haystack, string needle) {
        int m = haystack.size(), n = needle.size();
        for (int i = 0; i <= m - n; i++) {
            int j = 0;
            for (; j < n; j++) {
                if (haystack[i + j] != needle[j]) {
                    break;
                }
            }
            if (j == n) {
                return i;
            }
        }
        return -1;
    }
};
```

### KMP



```
class Solution
{
  public:
    int strStr(string haystack, string needle)
    {
        int m = haystack.size(), n = needle.size();
        if (!n)
            return 0;
        vector<int> lps = kmpProcess(needle);
        for (int i = 0, j = 0; i < m;)
        {
            if (haystack[i] == needle[j])
                i++, j++;
            if (j == n)
                return i - j;
            if (i < m && haystack[i] != needle[j])
                j ? j = lps[j - 1] : i++;
        }
        return -1;
    }

  private:
    vector<int> kmpProcess(string needle)
    {
        int n = needle.size();
        vector<int> lps(n, 0);
        for (int i = 1, len = 0; i < n;)
        {
            if (needle[i] == needle[len])
                lps[i++] = ++len;
            else if (len)
                len = lps[len - 1];
            else
                lps[i++] = 0;
        }
        return lps;
    }
};
```


## python


```

class Solution:
    def strStr(self, haystack: 'str', needle: 'str') -> 'int':
        for i in range(len(haystack) - len(needle) + 1):
            if haystack[i:i + len(needle)] == needle:
                return i
        return -1
```

