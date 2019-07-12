
# kickstar2016-Round.B-D 题解
https://code.google.com/codejam/contest/5254487/dashboard#s=p3
#### C++代码
```cpp
//
//  main.cpp
//
//  Created by ZhangJidong on 2019/6/11.
//  Copyright © 2019年 ZhangJidong. All rights reserved.
//
#include<bits/stdc++.h>
using namespace std;
typedef  long long int LL;
const int maxn = 5005;
int q, n, mod;
int fn_1[maxn];
int sumN[maxn], ans[maxn];
int jie[maxn];
int sum(int a, int b){
    int s = a + b;
    if(s >= mod)
        return s-mod;
    return s;
}
int sub(int a, int b){
    int s = a - b;
    if(s < 0)
        return s + mod;
    return s;
}
int mult(int a, int b){
    return (1LL * a * b % mod);
}
int power(int a, int b){
    if(b==0)
        return 1;
    int res = power(a, b/2);
    res = mult(res, res);
    if(b & 1)
        return mult(a, res);
    return res;
}
int inv(int a){
    return power(a, mod-2);
}

void solve(){
    ifstream cin("/Users/zhangjidong/Desktop/sodu/sodu/input.txt");
    ofstream cout("/Users/zhangjidong/Desktop/sodu/sodu/output.txt");
    cin>>q;
    
    for(int ca=1;ca<=q;ca++){
        cin >> n >> mod;
        if(mod==1){
            cout<<"Case #"<<ca<<": "<< 0 <<endl;
            continue;
        }
        memset(sumN,0,sizeof(sumN));
        memset(ans, 0, sizeof(ans));
        memset(fn_1, 0, sizeof(fn_1));
        memset(jie, 0, sizeof(jie));
        jie[1] = jie[0] = 1;fn_1[1] = 1; ans[1] = 1; sumN[1] = 1;
        for(int i=2;i<=n+1;i++){
            jie[i] = mult(jie[i-1], i);
        }
        for(int i=2;i<=n+1;i++){
            fn_1[i] = jie[i];
            for(int j=1;j<i;j++){
                fn_1[i] = sub(fn_1[i], mult(fn_1[j], jie[i-j]));
            }
            for(int j=1;j<=i;j++){
                sumN[i] = sum(sumN[i], mult(fn_1[j], sumN[i-j]+jie[i-j]));
            }
            for(int j=1;j<=i;j++){
                ans[i] = sum(ans[i], mult(fn_1[j], sum(sum(ans[i-j], mult(2, sumN[i-j])), jie[i-j])));
            }
        }
        cout<<"Case #"<<ca<<": "<<ans[n]<<endl;
    }
    
}

int main(){
    cin.sync_with_stdio(0);cin.tie(0);
    solve();
    
}



```


