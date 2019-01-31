## C++



```
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

