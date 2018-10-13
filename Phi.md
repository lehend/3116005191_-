#include <iostream>
#include <math.h>
#include <time.h>
#include <stdio.h>
#include <stdlib.h>
 
using namespace std;
 
 
 
unsigned long int a[10000]={2}, num=1;
unsigned long int j=0;
 
inline int prime(unsigned long int x)
{
 
    unsigned long int m;
    m=sqrt(x);
    for(j=2;j<m;j++)
    {
        if(x%j==0)
            return 0;
    }
    return 1;
}
 
 
 
int max_gongyue(int num1,int num2)
{
    int temp,m,n;
    if(num1<num2)
    {
        temp=num1;
        num1=num2;
        num2=temp;
    }
 
    m=num1;
    n=num2;
    while(m%n)
    {
        temp=m;
        m=n;
        n=temp-n*(temp/n);
    }
    return n;
}
 
 
int oula(int num)
{
    int sum=0;
    if(num==1)
    {
        return 1;
    }
 
    if(prime(num))
    {
        return num-1;
    }
    else
    {
        for(int i=1;i<=num-1;i++)
        {
            if(max_gongyue(i,num)==1)
            {
                sum++;
            }
        }
        return sum;
    }
}
int main()
{
    int n;
    cout<<"计算欧拉函数Φ(n)  "<<"请输入n"<<endl;
    while(cin>>n)
    {
        cout<<"Φ(n)="<<oula(n)<<endl;
    }
    return 0;
}
