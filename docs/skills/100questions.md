# 编程

## 1 回型矩阵

<img src="../images/image-20240721165121266.png" alt="image-20240721165121266" style="zoom:50%;" />

```c++
#include <iostream>
#include <vector>
using namespace std;
class Solutions{
public:
    void ShowMatrix(const vector<vector<int>>& matrix) {//输出矩阵
        int n = matrix.size();
        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < n; ++j)
                printf("%4d ", matrix[i][j]);
            cout << endl;
        }
    }
    vector<vector<int>> Clip(const int& n) {
        vector<vector<int>> clip(n, vector<int>(n));
        int left = 0, top = 0, right = n - 1, bottom = n - 1;
        int l, r, b, t;
        int num = 1;
        while (num <= n * n) {//循环条件可换top==bottom && left==right
            l = left;
            while (l <= right)
                clip[top][l++] = num++;
            ++top;
            t = top;
            while (t <= bottom)
                clip[t++][right] = num++;
            --right;
            r = right;
            while (r >= left)
                clip[bottom][r--] = num++;
            --bottom;
            b = bottom;
            while (b >= top)
                clip[b--][left] = num++;
            ++left;
        }
        return clip;
    }
};
int main() {
    int n;
    cin >> n;
    Solutions s;
    vector<vector<int>> m(n, vector<int>(n));
    m = s.Clip(n);
    s.ShowMatrix(m);
    return 0;
}
```

