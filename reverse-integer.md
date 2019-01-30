## C++



```
INT_MAX = 2147483647
INT_MIN = -2147483648
```



```
#include <iostream>
#include <vector>
using namespace std;

class Solution
{
  public:
    int reverse(int x)
    {
        int result = 0;
        while (x != 0)
        {
            int pop = x % 10;
            x /= 10;
            if (result > INT_MAX / 10 || (result == INT_MAX / 10 && pop > 7))
            {
                return 0;
            }
            if (result < INT_MIN / 10 || (result == INT_MIN / 10 && pop < -8))
            {
                return 0;
            }
            result = result * 10 + pop;
        }
        return result;
    }
};

int main()
{
    int x;
    cin >> x;
    Solution *s = new Solution();
    cout << s->reverse(x) << endl;
    cout << "Hello World!" << endl;
    cout << INT_MAX << endl;
    cout << INT_MIN << endl;
    system("pause");
    return 0;
}

```


