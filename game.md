INCLUDE Irvine32.inc
INCLUDE macros.inc
.DATA 
vardelay1 DWORD 80
lives DWORD 9
level DWORD 1
score dword 0
arrayballrow BYTE 15,14,13,12,11,10,9,8,7,6,5,4,3
x DWORD 20;man
y DWORD 26;man
str1 BYTE "YOU GOT IT!",0
col DWORD 0;ball
.CODE
MAIN PROC
mov eax,black+(9*16)
call settextcolor
call clrscr
call crlf
 call crlf
 call crlf
 call crlf
 call crlf
 call crlf
 call crlf
 call crlf
 call crlf 
 call crlf
 mWrite" !!!!!!!PRESS ENTER TO START THE GAME !!!!!!!"
 call crlf
 call crlf
 call crlf
 call crlf
 call crlf
 call crlf
 call crlf
 call crlf
 call crlf

 call ballmov

 et_::
 call clrscr
 call crlf
 call crlf
 call crlf
 call crlf
 call crlf
 call crlf
 call crlf
 call crlf
 call crlf
 mWrite" CONGRATULATIONS !"
 call crlf
 mWrite" !!!!!!!YOU WON THE GAME!!!!!!!"
 call crlf
 call crlf
 call crlf
 call crlf
 call crlf
 call crlf
 call crlf
 call crlf
 call crlf
 mov eax,1000
 call delay
 jmp l10
 ext_::
  call crlf
 call crlf
 call crlf
 call crlf
 call crlf
 call crlf
 call crlf
 call crlf
 call crlf
 mWrite" GAME OVER"
 call crlf
 mWrite" !!!!!!!YOU LOST THE GAME!!!!!!!"
 call crlf
 call crlf
 call crlf
 call crlf
 call crlf
 call crlf
 call crlf
 call crlf
 call crlf
 mov eax,1000
 call delay


 l10:
MAIN ENDP
exit
screen PROC uses eax
mov eax, level
cmp eax,1
je l1
cmp eax,2
je l2
cmp eax,3
je l3
cmp eax,4
je l4
jmp et_
l1:
mov eax, yellow + (gray*16)
jmp setting_
l2:
mov eax, yellow + (blue*16)
jmp setting_
l3:
mov eax, red + (white*16)
jmp setting_
l4:
mov eax, black + (3*16)
jmp setting_

setting_:
call SetTextColor
call clrscr
mWrite " ===================================================================================================="
call crlf
mWrite" Press a to move left d to move right and s for shooter"
call crlf
  mWrite "|| * BUBBLE TROUBLE GAME LEVEL : "
  mov eax,level
  call Writedec
  mWrite" * ||"
  call crlf
  mWrite"|| ||"
  call crlf
  mWrite "|| ||"
  call crlf
  mWrite "|| ||"
  call crlf
  mWrite "|| ||"
  call crlf
  mWrite "|| ||"
  call crlf
  mWrite "|| ||"
  call crlf
  mWrite "|| ||"
  call crlf
  mWrite "|| ||" 
  call crlf
  mWrite "|| ||"
  call crlf
  mWrite "|| ||"
  call crlf
  mWrite "|| ||"
  call crlf
  mWrite "|| ||"
  call crlf
  mWrite "|| ||"
  call crlf
  mWrite "|| ||"
  call crlf
  mWrite "|| ||"
  call crlf
  mWrite "|| ||"
  call crlf
  mWrite "|| ||"
  call crlf
  mWrite "|| ||"
  call crlf
  mWrite "|| ||"
  call crlf
  mWrite "|| ||"
  call crlf
  mWrite "|| ||"
  call crlf
  mWrite "|| ||"
  call crlf
  mWrite "|| --------------------------------------- ||"
  call crlf
  mWrite "|| ||"
  call crlf
  mWrite "|| | SCORE :"
  mov eax,score
  call Writeint
  mWrite" | ||"
  call crlf
  mWrite "|| | LIVES <3 :"

  mov eax,lives
  call writeint
  mWrite" | ||"
  call crlf
  mWrite "|| | | ||"
  call crlf
  mWrite " ===================================================================================================="
ret
screen endp

ballmov Proc
mov esi,-1
mov edx,0
L1:
inc esi
mov dh, arrayballrow[esi]
mov dl ,BYTE ptr col
call gotoxy
mov eax,'O'
call writechar
call drawman
call screen
call incdeccol
cmp dh,3
jg l1
l2:
dec esi
mov dh,BYTE ptr arrayballrow[esi]
mov dl ,BYTE ptr col
call gotoxy
mov eax,'O'
call writechar
call drawman
call screen
call incdeccol
cmp dh,15
je l1
jmp l2
ret
ballmov endp
drawman PROC uses esi eax ebx edx
 mov eax,0
 call readchar
 cmp eax,1E61h
 je l1
 cmp eax,2064h
 je l2
 cmp eax,1F73h
 pushfd
 mov ebx,y
 mov ecx,x
 dec lives
 mov eax, lives
 cmp lives,-1
 je ext_

 popfd
 jz arrow
 l2:
 mov edx,0
 mov dh,BYTE ptr x
 inc y
 inc y
 inc y
 mov dl,BYTE ptr y
 cmp dl,100
 jge ext_
 call gotoxy
 mov dl,BYTE ptr y
 call gotoxy
 mov eax,'0'
 call writechar
 mov dl,BYTE ptr y
 dec dl
 inc dh
 call gotoxy
 mov eax,'/'
 call Writechar
 mov dl,BYTE ptr y
 call gotoxy
 mov eax,'|'
 call writechar
 mov dl,BYTE ptr y
 inc dl
 call gotoxy
 mov eax,'\'
 call writechar
 mov dl,BYTE ptr y
 inc dh
 dec dl
 call gotoxy
 mov eax,'/'
 call writechar
 mov dl,BYTE ptr y
 inc dl
 call gotoxy
 mov eax,'\'
 call Writechar
 mov eax,200
 call delay
 jmp l3

 l1:
 mov edx,0
 mov dh,BYTE ptr x
 dec y
 dec y
 dec y
 mov dl,BYTE ptr y
 cmp dl,3
 jle ext_
 call gotoxy
 mov eax,'0'
 call writechar
 mov dl,BYTE ptr y
 dec dl
 inc dh
 call gotoxy
 mov eax,'/'
 call Writechar
 mov dl,BYTE ptr y
 call gotoxy
 mov eax,'|'
 call writechar
 mov dl,BYTE ptr y
 inc dl
 call gotoxy
 mov eax,'\'
 call writechar
 mov dl,BYTE ptr y
 inc dh
 dec dl
 call gotoxy
 mov eax,'/'
 call writechar
 mov dl,BYTE ptr y
 inc dl
 call gotoxy
 mov eax,'\'
 call Writechar
 mov eax,200
 call delay
 jmp l3
 arrow:
   
  while_:
  cmp ecx,3
  jle l3
  mov eax,col
  cmp dl,al
  je l5
  jmp l8
  l5:
  movzx eax,arrayballrow[esi]
  cmp cl,al
  je l4
  l8:
  mov eax,0
  mov eax,'|'
  mov dh,cl
  mov dl ,byte ptr y
  dec ecx
  call gotoxy
  call writechar
  jmp arrow
  l4:
   push edx
   mov edx ,offset str1
   call gotoxy
   call Writestring
   mov eax,100
   call delay
   pop edx
   inc score
   inc lives
   mov eax,score
   cmp eax,5
   jne l3
   inc level
   mov score,0
   sub vardelay1,10
   mov eax,9
   mov lives,eax

 l3:
 mov eax,100
 call delay


 ret
drawman endp
incdeccol PROC
cmp col,100
jge l2
jmp l3
l2:
mov col,3
jmp exit_
l3:
inc col
inc col
exit_:
ret
incdeccol endp
END MAIN
