        CODE  SEGMENT
              ASSUME    CS:CODE
           X  DW        60000
           Y  DW        5555
      START:
              PUSH      CS
              POP       DS
              PUSH      CS
              POP       ES
              MOV       AX,X
              MOV       BX,Y
              CALL      GCD
              CALL      DSPAX
               
              MOV       AH,4CH
              INT       21H
 
;=================================
         GCD  PROC      NEAR
              PUSH      DX
              PUSHF
              ; 两个数在 ax、bx中，结果在 ax中
              CMP       AX,BX
              JA        @GCD1
              XCHG      AX,BX       ; 把较大数交换到ax中
      @GCD1:
              MOV       DX,0
              DIV       BX
              CMP       DX,0
              JE        @GCD2
              MOV       AX,DX
              CALL      GCD
              JMP       @GCD3
      @GCD2:
              MOV       AX,BX
      @GCD3:
              POPF
              POP       DX
              RET
         GCD  ENDP
;================================
       DSPAX  PROC      NEAR
              PUSH      AX
              PUSH      BX
              PUSH      CX
              PUSH      DX
              PUSHF
              XOR       CX,CX
              MOV       BX,10
    @DSPAX1:
              XOR       DX,DX
              DIV       BX
              INC       CX
              OR        DX,30H
              PUSH      DX
              CMP       AX,0
              JNE       @DSPAX1
              MOV       AH,2
   @DISPAX2:
              POP       DX
              INT       21H
              LOOP      @DISPAX2
              MOV       DL,32
              INT       21H
              POPF
              POP       DX
              POP       CX
              POP       BX
              POP       AX
              RET
       DSPAX  ENDP
;====================================
        CODE  ENDS
              END       START