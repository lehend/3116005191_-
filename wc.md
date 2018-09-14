WC项目要求

　　这个项目要求写一个命令行程序，模仿已有的wc.exe的功能，并加以扩充，给出某程序设计源语言文件的字符数、单词数和行数。给实现一个统计程序，它能正确统计程序文件的字符数、单词数、行数，以及其他扩展功能，并能够快速的处理多个文件。

用户需求

　　程序员处理需求的模式为：wc.exe [paramter][file_name]

　　各个参数的意义：

　　基本功能列表：wc.exe -c file.c:char count;

　　　　　　　　　wc.exe -w file.c:char count;

　　　　　　　　　wc.exe -l file .c:line count;

　　扩展功能：-s 递归处理目录下符合条件的文件

　　　　　　　-a 返回高级选项（代码行、空行、注释行）

　　　　　　　　空行：本行全部是空格或者格式控制字符，如果包括代码，则只有不超过一个可显示的字符，例如“}”

　　　　　　　　代码行：本行包括多于一个字符的代码。

　　　　　　　　注释行：本行不是代码行，并且本行包括注释，例如：}//注释。这种情况下，这一行属于注释行。

　　　　　　　　[file_name]:文件的目录名，可以处理一般通配符。

　　　　　　　　文本文件，确定字/词/句

　　高级功能：-x参数 这个参数单独使用，如果命令行有这个参数，则程序会显示图形界面，用户可以通过界面选取单个文件，程序就会显示文件的字符数、行数等信息。

需求举例：wc.exe -s -a *.c  返回当前目录、子目录所有.c文件的代码行数，空行数，注释行数。


#include "stdio.h"
#include "string.h"
#include "stdlib.h"
 
int charcalculate=0;
 
int wordcalculate=0;
 
int linecalculate=0;
 
void calculate(char * file)
{
    FILE * fp;
    char a;
    if((fp=fopen(file,"r"))==NULL)
    {
        printf("read file failed！\n");
        exit(-1);
    }
    while(!feof(fp))
    {
        a=fgetc(fp);
        if(a!=' '&&a!='\n'&&a!='\t'&&a!=','&&a!='.'&&a!='!'&&a!=';'&&a!='=')
            charcalculate++;
        if(a==' '||a=='\n'||a=='\t'||a==','||a=='.'||a=='!'||a=='='||a==';')
            wordcalculate++;
        if(a=='\n'||a=='\t')
            linecalculate++;
    }
    linecalculate++;
    charcalculate--;         
    fclose(fp);
}
 
int main(int argc, char* argv[])             
{
    FILE *fp;
 
    calculate(argv[2]);
    while(1)
    {
        if((fp=fopen(argv[2],"r"))==NULL)
        {  
        printf("FileNull\n\n\n");
        scanf("%s%s%s",argv[0],argv[1],argv[2]);
        continue;
        }
        else if(!strcmp(argv[1],"-c"))                 
            printf("File:%sCharNum:%d\n",argv[2],charcalculate);
        else if(!strcmp(argv[1],"-w"))                  
            printf("File:%sWordNum:%d\n",argv[2],wordcalculate);
        else if(!strcmp(argv[1],"-l"))                
            printf("File:%sLineNum:%d\n",argv[2],linecalculate);
        else if(!strcmp(argv[1],"exit"))
        {
            printf("Exit!\n");
            break;
        }
        else
            printf("NullPoint\n");
        printf("\n\n");
        scanf("%s%s%s",argv[0],argv[1],argv[2]);
    }
    return 0;
     
}