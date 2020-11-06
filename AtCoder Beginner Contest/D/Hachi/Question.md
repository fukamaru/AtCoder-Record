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
_S_
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
**コード**

```
#include <bits/stdc++.h>
using namespace std;

#define FAST ios::sync_with_stdio(false);cin.tie(0);

bool solve()
{
  string s;
  cin >> s;
  
  if(s.size() == 1) return s == "8";
  if(s.size() == 2)
  {
      if(stoi(s) % 8 == 0) return 1;
      swap(s[0], s[1]);
      return stoi(s) % 8 == 0;
  }
  
  vector<int> cnt(10);
  for(char x: s) cnt[x - '0'] ++;
  for(int i = 112; i < 100; i += 8)
  {
      auto c = cnt;
      for(char x : to_string(i)) c[x - '0'] --;
      if(all_of(c.begin(), c.end(), [](int x) {return x >= 0; })) return 1;
  }
  return 0;
}

int main()
{
  int t = 1;
  while(t--)
  {
      puts(solves() ? "Yes" : "No");
  }
  return 0;
}
```
