# Hachi #
実行時間制限:2 sec / メモリ制限:1024 MB

**問題文**

'1'~'9'の数字のみからなる数字列_S_が与えられます。

蜂の高橋くんは、8の倍数が好きです。

高橋くんは、数字列_S_を並び替えて8の倍数を作ろうとしています。

8の倍数を作れるかどうか判定してください。


**制約**
+ $$
1 \ge\ left\| S \right\| \ge 2\times 10^5 
$$
+ _S_の各文字は'1'~'9'のいずれか

___
**入力**

入力は以下の形式で標準入力から与えられる。

```
$$_S_$$
```

**出力**

数字列_S_を並び替えて8の倍数を作れるなら'Yes'を、作れないなら'No'を出力せよ。

___
**入力例１**

```
1234
```

**出力例１**

```
Yes
```

**入力例２**

```
1333
```

**出力例２**

```
No
```

**入力例３**

```
8
```

**出力例３**

```
Yes
```
____

**アイデア**

题中要求给出一个1到100,000之间的整数，判断组成这个数的各位数字经过重新组合后能否为8的倍数。


____
**コード**

```
#include <bits/stdc++.h>
using namespace std;

#define FAST ios::sync_with_stdio(false);cin.tie(0);

bool solve()
{
  string s;
  cin >> s;
  
  //如果输入数字为个位数，只需判断其是否等于8
  if(s.size() == 1) return s == "8";
  //如果输入数字为两位数，只需判断其本身和十位数个位数互换后的两个数字是否为8的倍数即可
  if(s.size() == 2)
  {
      if(stoi(s) % 8 == 0) return 1;
      swap(s[0], s[1]);
      return stoi(s) % 8 == 0;
  }
  
  //最后考虑输入数字位数大于2的情况
  //创建一个向量用于储存输入数字中1～9每个数的出现次数
  vector<int> cnt(10);
  for(char x: s) cnt[x - '0'] ++;
  //利用for循环判断1～9出现次数与8的倍数之间的一致性，若一致则该输入数字可以组织为8的倍数的形式
  for(int i = 112; i < 1000; i += 8)
  {
      auto c = cnt;
      //复制存储出现次数的向量，并减去当前作为判断基准的倍数中相应数字的出现次数
      for(char x : to_string(i)) c[x - '0'] --;
      //若经过排列后可被8整除，则其和某个8的倍数中每个数字的出现次数均一致，即减去倍数中数字的出现次数之后，向量中存储的各项均为0
      if(all_of(c.begin(), c.end(), [](int x) {return x >= 0;})) return 1;
  }
  return 0;
}

int main()
{
  FAST
  int t = 1;
  while(t--)
  {
      puts(solves() ? "Yes" : "No");
  }
  return 0;
}
```
