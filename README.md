# Graph-drawer-in-assemnly
parabola and linear graph drawer in assembly X86
data segment
    
        x dw 160
        y dw 75
        color db 14  
        color1 db 9
        gt dw 0
        at db 0
        bsighn db 0
        msighn db 0  
        axp dw 0
        bxp dw 0                                               
        cxp dw 0
        ezer dw 0
        ezer2 dw 0    
        counter db 0 
        sign db 0   
        axsign db 0                                              
        bxsign db 0   
        cxsign db 0   
        msg db "What would you like to draw? for line press 1 for parabola press 2" , 0Dh,0Ah, 24h   
        pi1 db "Becuase there is limited range of pixels please note the intructions:" ,   0Dh,0Ah, 24h
        pi2 db "When you type the a you can put only one number.the first character should be a sign(+,-) and the other a number" ,   0Dh,0Ah, 24h        
        pi3 db "When you type the b you can put only two numbers.If you want to insert a one digit number, enter zero first and than the number.you can put a number in the range of 0<20 " , 0Dh,0Ah, 24h                                                                                                                     
        pi4 db "When you type the c you can put only two numbers.If you want to insert a one digit number, enter zero first and than the number.you can put a number in the range of 0<70" , 0Dh,0Ah, 24h                                                                   
        pi5 db "When you type the b you can put only two numbers.If you want to insert a one digit number, enter zero first and than the number.you can put a number in the range of 0<70" , 0Dh,0Ah, 24h
ends  


stack segment
    dw 128dup(0)
ends
code segment  
proc zirim ;drawing the zirim
    pusha 
    ; Print red dot
    mov cx,160 
    mov dx,0
    mov al,color1 
    mov ah,0ch
                                                      
 l2:   ; zir y
    int 10h
    inc dx
                                                   
                            
    cmp dx, X
    jne l2
    mov dx,y
    mov cx,80 
    mov al, color1 
    mov ah,0ch     
 l3:  ; zir  x
    
                
    int 10H
    inc cx       
    cmp cx, 240
    jnz l3 
    popa
ret
endp 

  
  
  
proc question   
    
    mov     dx,offset msg
    mov     ah, 09 
    int     21h     
ret 
endp
  
  
  
proc pmpb  
       ;drawing from zir y until the highest point
        e:   
        mov dx,160
        mov cx,160
           a:      
               
                sub cx,160 
                mov ax,[gt]  
                mul cx  
                mov bl,[at]
                add ax, bx
                mov dx,ax
                add cx,160
                add dx,160
                cmp dx,235
                jge n
                mov ax,235
                sub ax , dx
                mov dx , ax  
                mov al,color 
                mov ah,0ch   
                mov bh,0h
                int 10h
                inc cx
                jmp a 
                
                
                
             ;drawing from zir y until the lowest point    
            n:  
                mov dx,160
                mov cx,160 
            n1:
                
                sub cx,160 
                mov ax,[gt]
                mul cx  
                mov bl,[at]
                sub ax, bx
                mov dx,ax
                mov ax,160
                sub ax , cx
                mov cx , ax 
                mov ax,160
                sub ax , dx
                mov dx , ax  
                mov ax,235
                sub ax , dx
                mov dx , ax 
                cmp dx , 160
                jge end1
                mov al,color 
                mov ah,0ch   
                mov bh,0h
                int 10h
                mov ax,160
                sub ax , cx
                mov cx , ax 
                add cx,160
                inc cx
                
                jne n1
                
                end1:
ret
endp
   
  
  
  
   
proc nmpb    
    
    
              ;drawing from zir y until the lowest point
                  
                mov ch,[at]
                cmp ch,0
                jl nbnm           
                mov dx,160
                mov cx,160         
             k:              
                mov bh,0         
                sub cx,160 
                mov ax,[gt]  
                mul cx  
                mov bl,[at]
                add ax, bx
                mov dx,ax
                add cx,160
                mov ax,75
                sub ax , dx
                mov dx , ax
                cmp dx,150
                jge t
                mov al,color 
                mov ah,0ch   
                mov bh,0h
                int 10h
                inc cx          
                jmp k
                
               
               
                ;drawing from zir y until the highest point 
                
            t:   
                mov dx,160
                mov cx,160 
            t1:
                
                sub cx,160 
                mov ax,[gt]
                mul cx  
                mov bl,[at]
                sub ax, bx
                mov dx,ax
                mov ax,160
                sub ax , cx
                mov cx , ax 
                mov ax,160
                sub ax , dx
                mov dx , ax  
                mov ax,235
                sub ax , dx
                mov dx , ax
                cmp dx , 0
                jle end2  
                mov al,color 
                mov ah,0ch   
                mov bh,0h
                int 10h
                mov ax,160
                sub ax , cx
                mov cx , ax 
                add cx,160
                inc cx
                
                jne t1
                
                
                
                end2:
                
ret
endp
  
  
  
  

proc pmnb 
    
            ;drawing from zir y until the highest point
       
                mov dx,160
                mov cx,160
           bn1:      
               
                sub cx,160 
                mov ax,[gt]  
                mul cx  
                mov bl,[at]
                sub ax, bx
                mov dx,ax
                add cx,160
                add dx,160
                cmp dx,235
                jge h
                mov ax,235
                sub ax , dx
                mov dx , ax  
                mov al,color 
                mov ah,0ch   
                mov bh,0h
                int 10h
                inc cx
                jmp bn1    
                
            
              ;drawing from zir y until the lowest point   
                
            h:   
               mov dx,160
                mov cx,160
           f:      
                    
                sub cx,160 
                mov ax,[gt]  
                mul cx  
                mov bl,[at]
                add ax, bx
                mov dx,ax
                mov ax,160
                sub ax , cx
                mov cx , ax 
                mov ax,160
                sub ax , dx
                mov dx , ax  
                mov ax,235
                sub ax , dx
                mov dx , ax
                cmp dx , 160
                jge end3  
                mov al,color 
                mov ah,0ch   
                mov bh,0h
                int 10h
                mov ax,160
                sub ax , cx
                mov cx , ax 
                add cx,160
                inc cx
                jne f
                
                end3:
ret
endp
  
  
  
   
   
proc nmnb    
     ;drawing from zir y until the lowest point           
                
                neg ch
                mov [at],ch   
                mov dx,160
                mov cx,160         
             nbnm1: 
                mov bh,0         
                sub cx,160 
                mov ax,[gt]  
                mul cx  
                mov bl,[at]
                sub ax, bx
                mov dx,ax
                add cx,160
                
                mov ax,75
                sub ax , dx
                mov dx , ax
                cmp dx,150
                jge nbt
                   
                mov al,color 
                mov ah,0ch   
                mov bh,0h
                int 10h
                inc cx 
                jmp nbnm1
                
             
             
               ;drawing from zir y until the highest point
             nbt:         
                mov dx,160
                mov cx,160 
            nbt1:
                
                sub cx,160 
                mov ax,[gt]
                mul cx  
                mov bl,[at]
                add ax, bx
                mov dx,ax
                mov ax,160
                sub ax , cx
                mov cx , ax 
                mov ax,160
                sub ax , dx
                mov dx , ax  
                mov ax,235
                sub ax , dx
                mov dx , ax
                cmp dx , 0
                jle end4  
                mov al,color 
                mov ah,0ch   
                mov bh,0h
                int 10h
                mov ax,160
                sub ax , cx
                mov cx , ax 
                add cx,160
                inc cx
                
                jne nbt1   
                
                
                end4:

ret                
endp   

                          
proc MIZ
    mov dx, 75
    mov cx,90
    sub dl,[at]
    b:
       mov al,[color]
       mov ah,0ch
       int 10h
       inc cx
       mov si ,230
       cmp cx, si 
       jne b
ret
endp       
                            
                          

proc par3
     mov ax,2
            mov cx,[axp]
            mul cx
            neg ax
            mov cx,ax   
            mov ax,[bxp]
            mov dx,0
            div cx   
            mov [ezer],ax
            mov [ezer2],ax
            mul ax 
            mov cx,[axp]
            mul cx
            add ax,[cxp]
            mov bx,ax
            mov ax,[bxp]
            mov cx,[ezer]
            mul cx
            add bx,ax
         ;done
               
            mov ax, 13h
            int 10h
            call zirim 
            mov cx,160
            mov dx,75
            add cx,[ezer]
            sub dx,bx
            mov al,color 
            mov ah,0ch   
            mov bh,0h
            int 10h
            
            
            
         ;drawing from the right side of the parabola   
              
         
         an1:
            mov ax,[ezer]
            mul ax
            mov cx,[axp]
            mul cx
            add ax,[cxp]
            mov bx,ax
            mov ax,[ezer]
            mov cx,[bxp]
            mul cx
            add bx,ax
            mov cx,160
            mov dx,75
            add cx,[ezer]
            sub dx,bx
            mov al,color 
            mov ah,0ch   
            mov bh,0h
            cmp dx,195
            jge an2
            int 10h 
            inc [ezer]
            jmp an1
           
           
           ;drawing from the left side of the parabola
           
        an2:
            inc [ezer2]
        an3:
            mov ax,[ezer2]
            mul ax
            mov cx,[axp]
            mul cx
            add ax,[cxp]
            mov bx,ax
            mov ax,[ezer2]
            mov cx,[bxp]
            mul cx
            add bx,ax
            mov cx,160
            mov dx,75
            add cx,[ezer2]
            sub dx,bx
            mov al,color 
            mov ah,0ch   
            mov bh,0h
            cmp dx,195
            jge end5
            int 10h 
            dec [ezer2]
            jmp an3
            
            
            end5:
ret
endp            


proc par4
    mov ax,2
            mov cx,[axp]
            mul cx
            neg ax
            mov cx,ax   
            mov ax,[bxp]
            neg ax
            mov dx,0
            div cx
            neg ax   
            mov [ezer],ax
            mov [ezer2],ax
            mul ax 
            mov cx,[axp]
            mul cx
            add ax,[cxp]
            mov bx,ax
            mov ax,[bxp]
            mov cx,[ezer]
            mul cx
            add bx,ax
         ;done
               
            mov ax, 13h
            int 10h
            call zirim 
            mov cx,160
            mov dx,75
            add cx,[ezer]
            sub dx,bx
            mov al,color 
            mov ah,0ch   
            mov bh,0h
            int 10h  
           
           
           ;drawing from the right side of the parabola
           
         anbn1:
            mov ax,[ezer]
            mul ax
            mov cx,[axp]
            mul cx
            add ax,[cxp]
            mov bx,ax
            mov ax,[ezer]
            mov cx,[bxp]
            mul cx
            add bx,ax
            mov cx,160
            mov dx,75
            add cx,[ezer]
            sub dx,bx
            mov al,color 
            mov ah,0ch   
            mov bh,0h
            cmp dx,195
            jge anbn2
            int 10h 
            inc [ezer]
            jmp anbn1
            
            
            
            ;drawing from the left side of the parabola
           
        anbn2:
            inc [ezer2]
        anbn3:
            mov ax,[ezer2]
            mul ax
            mov cx,[axp]
            mul cx
            add ax,[cxp]
            mov bx,ax
            mov ax,[ezer2]
            mov cx,[bxp]
            mul cx
            add bx,ax
            mov cx,160
            mov dx,75
            add cx,[ezer2]
            sub dx,bx
            mov al,color 
            mov ah,0ch   
            mov bh,0h
            cmp dx,195
            jge end6
            int 10h 
            dec [ezer2]
            jmp anbn3
            
            end6:
            
ret
endp

   
   
   
   
proc par1
    ; nekudat kodkod -b div 2a 
       bz:
            mov ax,2
            mov cx,[axp]
            mul cx
            mov cx,ax   
            mov ax,[bxp]
            div cx     
            neg ax
            mov [ezer],ax
            mov [ezer2],ax
            mul ax 
            mov cx,[axp]
            mul cx
            add ax,[cxp]
            mov bx,ax
            mov ax,[bxp]
            mov cx,[ezer]
            mul cx
            add bx,ax
         ;done
               
            mov ax, 13h
            int 10h
            call zirim 
            mov cx,160
            mov dx,75
            add cx,[ezer]
            sub dx,bx
            mov al,color 
            mov ah,0ch   
            mov bh,0h
            int 10h 
           
           
           ;drawing from the right side of the parabola 
         
          bz1:
            mov ax,[ezer]
            mul ax
            mov cx,[axp]
            mul cx
            add ax,[cxp]
            mov bx,ax
            mov ax,[ezer]
            mov cx,[bxp]
            mul cx
            add bx,ax
            mov cx,160
            mov dx,75
            add cx,[ezer]
            sub dx,bx
            mov al,color 
            mov ah,0ch   
            mov bh,0h
            cmp dx,0
            jle bz2
            int 10h 
            inc [ezer]
            jmp bz1
            
            
            
          ;drawing from the left side of the parabola  
           
        bz2:
            inc [ezer2]
        bz3:
            mov ax,[ezer2]
            mul ax
            mov cx,[axp]
            mul cx
            add ax,[cxp]
            mov bx,ax
            mov ax,[ezer2]
            mov cx,[bxp]
            mul cx
            add bx,ax
            mov cx,160
            mov dx,75
            add cx,[ezer2]
            sub dx,bx
            mov al,color 
            mov ah,0ch   
            mov bh,0h
            cmp dx,0
            jle end7
            int 10h 
            dec [ezer2]
            jmp bz3
           end7:
ret
endp
   
   
   
   

proc par2
    mov ax,2
            mov cx,[axp]
            mul cx
            mov cx,ax   
            mov ax,[bxp]
            neg ax
            div cx
            mov [ezer],ax
            mov [ezer2],ax
            mul ax 
            mov cx,[axp]
            mul cx
            add ax,[cxp]
            mov bx,ax
            mov ax,[bxp]
            mov cx,[ezer]
            mul cx
            add bx,ax
         ;done
               
            mov ax, 13h
            int 10h
            call zirim 
            mov cx,160
            mov dx,75
            add cx,[ezer]
            sub dx,bx
            mov al,color 
            mov ah,0ch   
            mov bh,0h
            int 10h 
           
           
           ;drawing from the right side of the parabola 
         
          bnap1:
            mov ax,[ezer]
            mul ax
            mov cx,[axp]
            mul cx
            add ax,[cxp]
            mov bx,ax
            mov ax,[ezer]
            mov cx,[bxp]
            mul cx
            add bx,ax
            mov cx,160
            mov dx,75
            add cx,[ezer]
            sub dx,bx
            mov al,color 
            mov ah,0ch   
            mov bh,0h
            cmp dx,0
            jle bnap2
            int 10h 
            inc [ezer]
            jmp bnap1 
            
            
            
            ;drawing from the left side of the parabola
           
        bnap2:
            inc [ezer2]
        bnap3:
            mov ax,[ezer2]
            mul ax
            mov cx,[axp]
            mul cx
            add ax,[cxp]
            mov bx,ax
            mov ax,[ezer2]
            mov cx,[bxp]
            mul cx
            add bx,ax
            mov cx,160
            mov dx,75
            add cx,[ezer2]
            sub dx,bx
            mov al,color 
            mov ah,0ch   
            mov bh,0h
            cmp dx,0
            jle end8
            int 10h 
            dec [ezer2]
            jmp bnap3
           
           end8:
ret
endp           
   


proc klita_Line_Inst
     
        mov dl,0dh
        mov ah,2
        int 21h
        mov dl,0ah
        mov ah,2
        int 21h 
        mov     dx,offset pi1
        mov     ah, 09 
        int     21h
        
        mov     dx,offset pi2
        mov     ah, 09 
        int     21h
        
        mov     dx,offset pi5
        mov     ah, 09 
        int     21h
             ;
    ; input and print the function's body      
      restart1:
        mov dl,0dh
        mov ah,2
        int 21h
        mov dl,0ah
        mov ah,2
        int 21h 

    mov dl,'y'
    mov ah,2               
    int 21h
    mov dl,'='
    int 21h
    mov ah,1
    int 21h
    cmp al,'-'
    je mminus
     cmp al,'+'
    jne restart1
 m:    
    int 21h  
    cmp al,'9'
    jg restart1
    cmp al,'0'
    jl restart1
    sub al,30h
    mov ah,0 
    mov [gt],ax
    add al,30h
    cmp [msighn],1
    je ifmminus
 m1:  
    mov dl,'x'
    mov ah,2
    int 21h  
    mov ah,1 
    int 21h 
    cmp al,'-'
    je bminus
     cmp al,'+'
     jne restart1
  cont:  
    int 21h 
    cmp al,'6'
    jg restart1
    cmp al,'0'
    jl restart1
    sub al,30h
    mov dl,al
    mov dh,0
    mov ah,0
    mov al,10
    mul dx
    mov dx,ax
    add al,30h
    mov ah,1 
    int 21h  
    cmp al,'9'
    jg restart1
    cmp al,'0'
    jl restart1 
    sub al,30h
    mov [at],al
    add [at],dl
    add al,30h
    cmp [bsighn],2
    je ifbminus
    jmp strt
    
    
    mminus:
        mov [msighn],1
        jmp m
        
    ifmminus:
         mov cx,[gt]
         neg cx
         mov [gt],cx
         jmp m1
    bminus:
        mov [bsighn] ,2
        jmp cont         
    ifbminus:
        mov cl,[at]
        neg cl
        mov [at] ,cl  
ret 
endp




proc Parabola_Klita_Inst
       
        mov dl,0dh
        mov ah,2
        int 21h
        mov dl,0ah
        mov ah,2
        int 21h 
        mov     dx,offset pi1
        mov     ah, 09 
        int     21h
        
        mov     dx,offset pi2
        mov     ah, 09 
        int     21h
        
        mov     dx,offset pi3
        mov     ah, 09 
        int     21h
        
        mov     dx,offset pi4
        mov     ah, 09 
        int     21h 
    restart:
              mov dl,0dh
        mov ah,2
        int 21h
        mov dl,0ah
        mov ah,2
        int 21h 
        mov dl,'y'
        mov ah,2               
        int 21h
        mov dl,'='
        int 21h
        mov ah,1
        int 21h
        cmp al,'-' 
        je axminus
        cmp al,'+'
        jne restart
      a1:                                                                                                    
        int 21h
        cmp al,'9'
        jg restart
        cmp al,'0'
        jl restart  
        sub al,30h
        mov ah,0 
        mov [axp],ax
        add al,30h
        cmp [axsign],1
        je ifaxminus
     a2: 
        mov dl,'x'
        mov ah,2               
        int 21h
        mov dl,'^'
        int 21h   
        mov dl,'2'
        int 21h   
        mov ah,1
        int 21h
        cmp al,'-'
        je bxminus
        cmp al,'+'
        jne restart
      b1: 
        int 21h
         cmp al,'2'
        jge restart
        cmp al,'0'
        jl restart
        sub al,30h
        mov ah,0 
        mov [bxp],ax
        mov cx,10
        mov ah,0
        mul cx
        mov [bxp],ax
        add al,30h
        mov ah,1
        int 21h
         cmp al,'9'
        jg restart
        cmp al,'0'
        jl restart
        mov ah,0
        sub al,30h
        add [bxp],ax
        cmp [bxsign],1
        je ifbxminus
      b2: 
        mov dl,'x'
        mov ah,2               
        int 21h
        mov ah,1
        int 21h
        cmp al,'-'
        je cxminus
           cmp al,'+'
        jne restart
      c1:
        int 21h
         cmp al,'7'
        jge restart
        cmp al,'0'
        jl restart
        sub al,30h
        mov ah,0 
        mov [cxp],ax
        mov cx,10
        mov ah,0
        mul cx
        mov [cxp],ax
        add al,30h
        mov ah,1
        int 21h 
         cmp al,'9'
        jg restart
        cmp al,'0'
        jl restart
        mov ah,0
        sub al,30h
        add [cxp],ax
        cmp [cxsign],1
        je ifcxminus 
        jmp comp   
        
         
        
        axminus:
            mov [axsign],1
            jmp a1
        ifaxminus:
             mov cx,[axp]
             neg cx
             mov [axp],cx
             mov cx,0
             jmp a2
        bxminus:
            mov [bxsign],1
            jmp b1
        ifbxminus:
             mov cx,[bxp]
             neg cx
             mov [bxp],cx
             mov cx,0
             jmp b2
        cxminus:
            mov [cxsign],1
            jmp c1
            
        ifcxminus:
            mov cx,[cxp]
             neg cx
             mov [cxp],cx
             mov cx,0
                
ret
endp    
       
start:        
    mov ax, data
    mov ds, ax
    
    call question 
press: ;what to draw. parabola or line     
    mov ah,1
    int 21h
    cmp al,'2'
    je parabola  
    cmp al,'1'
    je line
   
    jmp press
     
     
     
     line:
        call klita_Line_Inst     ;Inputting the line function
     ; Graphic mode
    strt: 
    mov ax, 13h
    int 10h
     
    call zirim        
         
                
    cmp [gt],0
    je mz
    cmp [gt],0
    jl L
    cmp [at],0
    jl d
    jmp E1
     
  d: ; if b is negtive <nekudat hituh with zir y>  
             mov ch,[at]
             neg ch
             mov [at], ch 
             jmp bn
             
           
          E1:      
            call pmpb     ;drawing a line with positive m and negative b
            jmp c   
                
                
            bn:   
              call pmnb
              jmp c
              
                  ;drawing a line with positive m and negative b  
                 
                mz:   ;if m is 0 (shipua>
                    call MIZ
                    jmp c
                    
                    
                    
             L: 
               call nmpb    ;drawing a line with negative m and positive b
               jmp c 
                
                    
                
             nbnm:       ;drawing a line with negative m and negative b
                 call nmnb
                 jmp c
                
                
         
             
     parabola:
        call Parabola_Klita_Inst          
                               ;Inputting the parabola function
        
             
     comp:             
        
       cmp [axp],0
       jl an     
       cmp [bxp],0
       jl bnap
       
       
                
                
       call par1    ;drawing parabola with positive a and positive b     
         jmp c       
                
                
          bnap:
              call par2     ;drawing parabola with positive a and negative b
                
                jmp c
                
                
                
                
                
                
       
       
        an:
            cmp [bxp],0
            jl anbn 
            call par3   ;drawing parabola with negative a and positive b
             jmp c
            
            
            
       
       
       
       
       
         anbn: 
             call par4     ;drawing parabola with negative a and negative b
              jmp c  
               
   c: 
        mov ax, 04cH
        int 21H
               
  END start     
end
