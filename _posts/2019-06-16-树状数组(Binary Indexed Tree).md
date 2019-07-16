

# 树状数组

#### c++代码
```c++
//涉及区间查询就必须有D1，D2，此时单点更新可以认为是长度为1的区间更新，C可以用
//sum数组来代替
//sum(A,i) = sum(A_ori,i) + (i+1) * sum(d1, i)-sum(d2,i)  d2[i]=i*d1[i]
//update(l,r,val) ⇒ d1[l] += val d1[r+1] += -val  d2[l] += l*val d2[r+1] += (r+1)*(-val)
#define lowbit(i) (i & (-i))
typedef long long int LL;
const int maxn=1e5+5;
LL n;
LL C[maxn], D1[maxn], D2[maxn];
void update(LL* array, LL i, LL val){
	while(i<=n){
		array[i]+=val;
		i+=lowbit(i);
}
}
LL query(LL* array, LL i){
	LL ans = 0;
	while(i){
		ans += array[i];
		i -= lowbit(i);
}
return ans;
}
void update(LL l, LL r, LL val){
	update(D1, l, val);
	update(D1, r+1, -val);
	update(D2, l, l*val);
	update(D2, r+1, -(r+1) * val);
}
void update(LL i, val){
	update(C, i, val);
}
LL query(LL i){
	return query(C, i) + (i+1) * query(D1,i) - query(D2,i);
}
LL query(LL l, LL r){
	return query(r) - query(l-1);
}

```

