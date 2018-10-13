#include <iostream>
#include <cstdio>
 
 
using namespace std;
 
 
//模的指数运算
int modexp(int x,int y,int N);//x为底数，y为指数，N为取模的数字
 
 
int main()
{
   int x,y,N;
   int ans;
   cin>>x>>y>>N;
   ans=modexp(x,y,N);
   cout<<ans<<endl;
    return 0;
}
 
 
int modexp(int x,int y,int N)
{
     if(y==0) return 1;
     int z=modexp(x,y/2,N);
     if(y%2==0) return z*z % N;
     else return x*z*z % N;
}
