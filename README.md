# stepper-motor-using-8086-processor
TITLE MASM Template
INCLUDE Irvine32.inc
.data
myMessage BYTE "if you want to turn on the the motor enter 1 if you want to turn it
off enter 0 ",0
myMessage1 BYTE "enter full stepmode (0) or half stepmode (1) ",0
myMessage2 BYTE "adjust the potentiometer to enter the delay time you want",0
myMessage3 BYTE "enter the direction clockwise (0) or anti clockwise(1) ",0
myMessage4 BYTE "enter themaximum delay value that the motor can handle ",0
stepMode DWORD ?
DelayTime DWORD ?
switch DWORD ?
direction DWORD ?
maxValue DWORD ?
speedDisplay DWORD ?
.code
main proc
mov edx, offset myMessage
call writestring
call readint
mov switch, eax
beginwhile:
.IF switch == 0
jnl endwhile
.ENDIF
mov edx, offset myMessage1
call writestring
call readint
mov stepMode, eax
mov edx, offset myMessage2
call writestring
call readint
mov DelayTime, eax
mov edx, offset myMessage3
call writestring
call readint
mov direction, eax
mov edx, offset myMessage4
call writestring
call readint
mov maxValue, eax
mov eax, DelayTime
imul eax, 100
mov edx,0
mov ecx ,maxValue
div ecx
imul eax,-1
add eax, 128
call writeint
mov edx, offset myMessage
call writestring
call readint
mov switch, eax
.IF switch == 1
jmp beginwhile
.ENDIF
endwhile:
exit
main endp
end main
