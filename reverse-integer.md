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


## python



```
class Solution:
    def reverse(self, x):
        """
        :type x: int
        :rtype: int
        """
        sign = 1 if x > 0 else -1
        x = x * sign
        str_x = list(str(x))[::-1]
        x = int("".join(str_x))
        return x * sign if x < 2**31 else 0

```


### python 将列表反序
reverse_list = list[::-1]
