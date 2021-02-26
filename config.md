<h3>Gera apenas codigo de montagem</h3>
$ gcc -m32 -S true.c
$ gcc -m32 -S false.c

//Codigo de montagem para 'TRUE'
int main(void)
{
  return 0;
}

	.text
.globl _main
_main:
	pushl	%ebp
	movl	%esp, %ebp
	subl	$8, %esp
	movl	$0, %eax
	leave
	ret
	.subsections_via_symbols
  
  
  
//Codigo de montagem para 'FALSE'
  int main(void)
{
  return 1;
}

	.text
.globl _main
_main:
	pushl	%ebp
	movl	%esp, %ebp
	subl	$8, %esp
	movl	$1, %eax
	leave
	ret
	.subsections_via_symbols
  
<h3>Diretrizes</h3>
  .text = codigo puro de maquina
  
  .globl _main = o mesmo que main(void)
  
  .subsections_via_symbols = nem usa mano(por enquanto)
  

<h3>Ex de Somatorio</h3>
  int somatorio(int n)
{
  int soma = 0;
  int i;

  for (i = 0; i < n; i++)
    soma = soma + i;

  return soma;
}

	.text
.globl _somatorio
_somatorio:
	pushl	%ebp
	movl	%esp, %ebp
	subl	$24, %esp
	movl	$0, -12(%ebp)
	movl	$0, -16(%ebp)
	jmp	L2
L3:
	movl	-16(%ebp), %eax
	addl	%eax, -12(%ebp)
	incl	-16(%ebp)
L2:
	movl	-16(%ebp), %eax
	cmpl	8(%ebp), %eax
	jl	L3
	movl	-12(%ebp), %eax
	leave
	ret
	.subsections_via_symbols
  
  
