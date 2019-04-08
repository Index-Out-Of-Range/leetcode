# Palindrome Number

## C++

```text
#include <iostream>
using namespace std;

class Solution
{
  public:
    bool isPalindrome(int x)
    {
        if (x < 0 || (x % 10 == 0 && x != 0))
            return false;
        int result = 0, temp = x;
        while (temp > 0)
        {
            result = result * 10 + temp % 10;
            temp /= 10;
        }
        return result == x;
    }
};

int main()
{
    Solution *s = new Solution();
    cout << s->isPalindrome(20) << endl;
    system("pause");
    return 0;
}
```

### 只判断数字的一半

```text
class Solution
{
  public:
    bool isPalindrome(int x)
    {
        if (x < 0 || (x % 10 == 0 && x != 0))
            return false;
        int result = 0;
        while (x > result)
        {
            result = result * 10 + x % 10;
            if (x == result)
                return true;
            x /= 10;
        }
        return result == x;
    }
};
```

## python

```text
class Solution:
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        if x < 0 or (x % 10 == 0 and x != 0):
            return False
        str_x = list(str(x))
        int_x = int("".join(str_x[::-1]))
        return int_x == x
```

### a little faster

```text
class Solution:
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        if x < 0 or (x % 10 == 0 and x != 0):
            return False
        str_x = str(x)
        i, j = 0, len(str_x) - 1
        while (i <= j):
            if str_x[i] != str_x[j]:
                return False
            i += 1
            j -= 1
        return True
```

