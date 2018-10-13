data segment
    Val dw 100  
    msg1 db 'Yes$'  
    msg2 db 'No$'  
data ends  

code segment  
    assume cs:code,ds:data  
start:  
    mov ax,data  
    mov ds,ax  

    mov bx,Val
    call judge  
    call crlf  
    mov ah,4ch  
    int 21h  

judge proc near  
    mov cx,bx  
    sub cx,2   
    cmp bx,2  
    jle print1  
    mov dl,1  
pri:  
    mov ax,bx  
    inc dl  
    div dl  
    cmp ah,0  
    jz print2  
    loop pri  
    jmp print1  
print1:  
    mov ah,09h  
    lea dx,msg1  
    int 21h  
    ret  
print2:  
    mov ah,09h  
    lea dx,msg2  
    int 21h       
ret  
judge endp  

crlf proc near  
    mov dl,0dh  
    mov ah,02h  
    int 21h  
    mov dl,0ah  
    mov ah,02h  
    int 21h    
ret  
crlf endp  

code ends  
    end start  