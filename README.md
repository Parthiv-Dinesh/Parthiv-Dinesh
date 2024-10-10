- 👋 Hi, I’m @Parthiv-Dinesh
- 👀 I’m interested in .
- 🌱 I’m currently learning python
- 💞️ I’m looking to collaborate on pyhton based projects
- 📫 How to reach me via parthivdinesh5946@gmail.com
- ⚡ Fun fact: Coding leads to great cognitive benefits.

<!---
Parthiv-Dinesh/Parthiv-Dinesh is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
#include<stdio.h>
#include<string.h>
#include<stdlib.h>
void main(){
char opcode[20],operand[20],symbol[20],label[20],code[20],mnemonic[25],character,add[20],objectcode[20];
int flag,flag1,locctr,location,loc;
FILE *fp1, *fp2, *fp3, *fp4;
fp1=fopen("out.txt","r");
fp2=fopen("assmlist.txt","w");
fp3=fopen("optab.txt","r");
fp4=fopen("symtab.txt","r");
fscanf(fp1, "%s%s%s", label, opcode, operand);
if(strcmp(opcode, "START")==0)
{
fprintf(fp2,"%s\t%s\t%s\n", label, opcode, operand);
fscanf(fp1, "%d %s\t%s\t%s",&locctr,label, opcode, operand);
}
while(strcmp(opcode, "END")!=0)
{
flag=0;
fscanf(fp3, "%s%s", code, mnemonic);
while(strcmp(code, "END")!=0)
{
if((strcmp(opcode, code) == 0) && (strcmp(mnemonic, "*"))!=0)
{
flag=1;
break;
}
fscanf(fp3,"%s%s",code,mnemonic);
}
if(flag==1)
{
flag1=0;
rewind(fp4);
while(!feof(fp4))
{
fscanf(fp4,"%s%d",symbol,&loc);
if(strcmp(symbol,operand)==0)
{
flag1=1;
break;
}
}
if(flag==1)
{
sprintf(add,"%d",loc);
strcpy(objectcode,strcat(mnemonic,add));
}
}
else if(strcmp(opcode,"BYTE")==0 || strcmp(opcode, "WORD")==0)
{
if((operand[0]=='C' || (operand[0]=='X')))
{
character = operand[2];
sprintf(add,"%d",character);
strcpy(objectcode,add);
}
else{
strcpy(objectcode,operand);
}
}
else
strcpy(objectcode, "\0");
fprintf(fp2,"%s\t%s\t%s\t%d\t%s\n", label, opcode, operand, locctr, objectcode);
fscanf(fp1,"%d %s%s%s",&locctr,label,opcode,operand);
}
fprintf(fp2,"%s\t%s\t%s\t%d\n",label,opcode,operand,locctr);
fclose(fp1);
fclose(fp2);
fclose(fp3);
fclose(fp4);
}