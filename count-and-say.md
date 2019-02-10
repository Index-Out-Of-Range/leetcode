## C++

### 递归



```
class Solution
{
  public:
    string countAndSay(int n)
    {
        if (n == 1)
            return "1";
        else if (n == 2)
            return "11";
        else
        {
            string temp = countAndSay(n - 1);
            string result = "";
            int count = 1;
            int n = temp.size();
            char ch = temp[n - 1];
            for (int i = n - 2; i >= 0; i--)
            {
                if (temp[i] != ch)
                {
                    result = to_string(count) + ch + result;
                    count = 1;
                    ch = temp[i];
                }
                else
                {
                    count++;
                }
            }
            result = to_string(count) + ch + result;
            return result;
        }
    }
};
```


### faster



```
class Solution
{
  public:
    string countAndSay(int n)
    {
        if (n == 0)
            return "";
        string result = "1";
        while (--n)
        {
            string temp = "";
            for (int i = 0; i < result.size(); i++)
            {
                int count = 1;
                while (i + 1 < result.size() && (result[i] == result[i + 1]))
                {
                    count++;
                    i++;
                }
                temp += to_string(count) + result[i];
            }
            result = temp;
        }
        return result;
    }
};
```




### stringstream
* 头文件：sstream


```
class Solution
{
  public:
    string countAndSay(int n)
    {
        string result = "1";
        for (int i = 1; i < n; ++i)
        {
            stringstream next;
            char u;
            int count = 0;
            for (const char &c : result)
            {
                if (count == 0)
                {
                    u = c, count = 1;
                }
                else if (u != c)
                {
                    next << count << u;
                    u = c, count = 1;
                }
                else
                {
                    count++;
                }
            }
            if (count != 0)
            {
                next << count << u;
            }
            result = next.str();
        }
        return result;
    }
};
```

