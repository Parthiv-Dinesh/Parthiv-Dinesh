- 👋 Hi, I’m @Parthiv-Dinesh
- 👀 I’m interested in .
- 🌱 I’m currently learning python
- 💞️ I’m looking to collaborate on pyhton based projects
- 📫 How to reach me via parthivdinesh5946@gmail.com
- ⚡ Fun fact: Coding leads to great cognitive benefits.



.model small
.stack 100h
.data
array dw 6,7,3,5,8,6,2,7,4,9,1
n dw 10
target dw 3
found db 0
msgfound db 'number found','$'
msgnotfound db 'number not found','$'
space dw ' ','$'

.code
main proc
mov ax,@data
mov ds,ax


mov cx,n
dec cx

outer_loop:
mov si,0
mov di,0
mov bx,cx
add bx,bx

inner_loop:
mov ax,array[si]
mov dx,array[si+2]
cmp ax,dx

jbe no_swap

;swap elements
mov array[si],dx
mov array[si+2],ax

no_swap:
add si,02h
cmp si,bx
jb inner_loop
dec cx
jnz outer_loop
mov cx,n
mov si,0

print_loop:
mov ax,array[si]
add ax,30h
mov dx,ax
mov ah,02h
int 21h
lea dx,space
mov ah,09h
int 21h
add si,02h
loop print_loop
mov cx,n
mov si,0
mov ax,target

search_loop:
mov dx,array[si]
cmp ax,dx
je found_element
add si,02h
loop search_loop

not_found:
lea dx,msgnotfound
mov ah,09h
int 21h
jmp end_program

found_element:
lea dx,msgfound
mov ah,09h
int 21h

end_program:
mov ah,4ch
int 21h
main endp
end main
