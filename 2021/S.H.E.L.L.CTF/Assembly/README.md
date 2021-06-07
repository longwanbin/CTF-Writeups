Question:

fun1(0x74,0x6f) + fun1(0x62,0x69) = ? Note : submit flag in hexadecimal format (e.g. 0x123dead) and wrap it in SHELL{ & }.

fun1:
	<+0>:	push   ebp
	<+1>:	mov    ebp,esp
	<+3>:	sub    esp,0x10
	<+6>:	mov    eax,DWORD PTR [ebp+0xc]
	<+9>:	mov    DWORD PTR [ebp-0x4],eax
	<+12>:	mov    eax,DWORD PTR [ebp+0x8]
	<+15>:	mov    DWORD PTR [ebp-0x8],eax
	<+18>:	jmp    <fun1+28>
	<+20>:	add    DWORD PTR [ebp-0x4],0x7
	<+24>:	add    DWORD PTR [ebp-0x8],0x70
	<+28>:	cmp    DWORD PTR [ebp-0x8],0x227
	<+35>:	jle    <fun1+20>
	<+37>:	mov    eax,DWORD PTR [ebp-0x4]
	<+40>:	leave  
	<+41>:	ret  


Writeups:
fun1:
	<+0>:	push   ebp                      ;   
	<+1>:	mov    ebp,esp                  ;
	<+3>:	sub    esp,0x10                 ;
	<+6>:	mov    eax,DWORD PTR [ebp+0xc]  ; eax = arg2
	<+9>:	mov    DWORD PTR [ebp-0x4],eax  ; temp = eax
	<+12>:	mov    eax,DWORD PTR [ebp+0x8]  ; eax = arg1
	<+15>:	mov    DWORD PTR [ebp-0x8],eax  ; temp2 = eax
	<+18>:	jmp    <fun1+28>                ; if (temp2 <= 0x227) {
	<+20>:	add    DWORD PTR [ebp-0x4],0x7  ;     temp1 += 0x7
	<+24>:	add    DWORD PTR [ebp-0x8],0x70 ;     temp2 += 0x70
	<+28>:	cmp    DWORD PTR [ebp-0x8],0x227; }
	<+35>:	jle    <fun1+20>
	<+37>:	mov    eax,DWORD PTR [ebp-0x4]  ; eax = temp1
	<+40>:	leave  
	<+41>:	ret
	
fun1(0x74,0x6f) + fun1(0x62, 0x69)

0x74,0x6f -> 0xe4,0x76 -> 0x154,0x7d -> 0x1c4,0x84 -> 0x234,0x8b

0x62,0x69 -> 0xd2,0x70 -> 0x142,0x77 -> 0x1b1,0x7e -> 0x221,0x85 -> 0x291,0x8c 

fun1(0x74,0x6f) + fun1(0x62, 0x69) = 0x8b + 0x8c = 0x117
