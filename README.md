# Homework19

extern printf
extern scanf
extern exit


section .data
	Input_num1 db "Enter the number 1",0
	Input_num2 db "Enter the number 2",0
	Input_operant db "Select  the Operant(1:Add,2:Sub,3:Mul,4:Div)",0
	result db "The resalt is:%d",10,0
	error db "Zero is not allowed",10,0
	format_int db"%d",0
section .bss
	num1 resd 1
	num2 resd 1
	operant resd 1
	res resd 1
section .text

	global_main

main:
	push Input_num1
	call printf
	add esp, 4
	
	push num1
	push format_int 
	call scanf 
	add esp,8
	
	push Input_num2
	call printf
	add esp,4
	
	push num2
	push format_int
	call scanf
	add esp,8

	push Input_operant
	call printf
	add esp,4
	
	push  operant
	push format_int
	call scanf
	add esp,8
	
	mov eax,[operant]
	cmp eax ,1
	je add
	cmp eax ,2
	je div
	cmp eax,3
	je mul
	cmp eax ,4
	je div
	jmp exit_program
	
add:
	mov eax,[num1]
	add eax,[num2]
	mov [res],eax
	jmp display_res
	
sub:
	mov eax,[num1]
	sub eax,[num2]
	mov [res],eax
	jmp display_res
mul:
	mov eax,[num1]
	imul eax,[num2]
	mov [res],eax
	jmp display_res
div:
	
	cmp eax,0
	je error_ziro
	mov rax,[num1]
	idiv [num2]
	mov [res],rax
	jmp display_res
	
error_ziro:
	push error
	call printf
	add esp,4
	jmp exit_program

display_res:
	push word[res]
	push result
	call printf
	add esp,8

exit_program:
	push 0
	call exit

	ret	
		
	
	
