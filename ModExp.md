#include <iostream>
#include <cstdio>
 
 
using namespace std;
 
 
//ģ��ָ������
int modexp(int x,int y,int N);//xΪ������yΪָ����NΪȡģ������
 
 
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
