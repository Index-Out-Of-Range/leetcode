## C++



```
#include <iostream>
#include <stack>
#include <unordered_map>
using namespace std;

class Solution
{
  public:
    bool isValid(string s)
    {
        if (s.size() == 0)
            return true;
        unordered_map<char, char> T = {{'(', ')'}, {'[', ']'}, {'{', '}'}};
        stack<char> bracket_stack;
        int i = 1;
        bracket_stack.push(s[0]);
        while (i < s.size())
        {
            if (s[i] == '(' || s[i] == '[' || s[i] == '{')
            {
                bracket_stack.push(s[i++]);
            }
            else
            {
                if (bracket_stack.empty())
                    return false;
                if (s[i] == T[bracket_stack.top()])
                {
                    bracket_stack.pop();
                    i++;
                }
                else
                {
                    return false;
                }
            }
        }
        return bracket_stack.empty() && i == s.size();
    }
};

int main()
{
    Solution *s = new Solution();
    cout << s->isValid("([)]") << endl;
    // system("pause");
    return 0;
}
```


```

class Solution
{
  public:
    bool isValid(string s)
    {
        stack<char> bracket_stack;
        for (char c : s)
        {
            if (c == '(' || c == '[' || c == '{')
            {
                bracket_stack.push(c);
            }
            else
            {
                if (bracket_stack.empty())
                    return false;
                if (c == ')' && bracket_stack.top() != '(')
                    return false;
                if (c == ']' && bracket_stack.top() != '[')
                    return false;
                if (c == '}' && bracket_stack.top() != '{')
                    return false;
                bracket_stack.pop();
            }
        }
        return bracket_stack.empty();
    }
};
```


## python



```
class Solution:
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        stack = []
        dict = {")": "(", "]": "[", "}": "{"}
        for c in s:
            if c in dict:
                top_element = stack.pop() if stack else 'err'
                if dict[c] != top_element:
                    return False
            else:
                stack.append(c)
        return not stack

```

