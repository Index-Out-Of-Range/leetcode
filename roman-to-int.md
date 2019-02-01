## C++


```

class Solution
{
  public:
    int romanToInt(string s)
    {
        int result = 0;
        for (int i = 0; i < s.length(); i++)
        {
            if (s[i] == 'I')
            {
                if (s[i + 1] == 'V')
                {
                    result = result + 4;
                    i++;
                }
                else if (s[i + 1] == 'X')
                {
                    result = result + 9;
                    i++;
                }
                else
                    result = result + 1;
            }
            else if (s[i] == 'V')
            {
                result = result + 5;
            }
            else if (s[i] == 'X')
            {
                if (s[i + 1] == 'L')
                {
                    result = result + 40;
                    i++;
                }
                else if (s[i + 1] == 'C')
                {
                    result = result + 90;
                    i++;
                }
                else
                    result = result + 10;
            }
            else if (s[i] == 'L')
            {
                result = result + 50;
            }
            else if (s[i] == 'C')
            {
                if (s[i + 1] == 'D')
                {
                    result = result + 400;
                    i++;
                }
                else if (s[i + 1] == 'M')
                {
                    result = result + 900;
                    i++;
                }
                else
                    result = result + 100;
            }
            else if (s[i] == 'D')
            {
                result = result + 500;
            }
            else if (s[i] == 'M')
            {
                result = result + 1000;
            }
        }
        return result;
    }
};
```


### 使用unordered_map


```
class Solution
{
public:
	int romanToInt(string s)
	{
		unordered_map<char, int> T = {
			{'I',1},
			{'V',5},
			{'X',10},
			{'L',50},
			{'C',100},
			{'D',500},
			{'M',1000}
		};
		int result = T[s.back()];
		for (int i = s.length() - 2; i >= 0; i--)
		{
			if (T[s[i]] < T[s[i + 1]])
				result -= T[s[i]];
			else
				result += T[s[i]];
		}
		return result;
	}
};
```



```
class Solution
{
public:
	int romanToInt(string s)
	{
		int temp = 0, right = 0, left = 0;
		for (auto c = s.rbegin(); c != s.rend(); c++)
		{
			switch (*c)
			{
			case 'I': left = 1; break;
			case 'V': left = 5; break;
			case 'X': left = 10; break;
			case 'L': left = 50; break;
			case 'C': left = 100; break;
			case 'D': left = 500; break;
			case 'M': left = 1000; break;
			default: break;
			}
			left >= temp ? right += left : right -= left;
			temp = left;
		}
		return right;
	}
};
```


