- 👋 Hi, I’m @Parthiv-Dinesh
- 👀 I’m interested in .
- 🌱 I’m currently learning python
- 💞️ I’m looking to collaborate on pyhton based projects
- 📫 How to reach me via parthivdinesh5946@gmail.com
- ⚡ Fun fact: Coding leads to great cognitive benefits.



READ MACRO 
MOV AH,3FH 
LEA DX,A 
INT 21H 
ENDM 
DISP MACRO B 
MOV AH,09H 
LEA DX,B 
INT 21H 
ENDM 
.MODEL SMALL 
.STACK 
.DATA 
MSG1 DB 0AH,0DH,”Enter the first string:$” 
MSG2 DB 0AH,0DH,”Enter the second string:$” 
MSG3 DB 0AH,0DH,”New string:$” 
STR1 DB 100 DUP(“$”) 
STR2 DB 100 DUP(“$”) 
.CODE 
START 
MOV AX,@DATA 
MOV DS,AX 
MOV SI,00H 
MOV DI,00H 
DISP MSG1 
READ STR1 
SUB AX,02H 
MOV SI,AX 
DISP MSG2 
READ STR2 
DISP MSG3 
L1: 
 CMP STR2[DI],”$” 
 JNE L2 
 DISP STR1 
 JMP L3 
L2: 
 MOV AH,STR2[DI] 
 MOV STR1 [SI],AH 
 INC SI 
 INC DI
LOOP L1 
L3: 
 END START