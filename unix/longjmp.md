# longjmp && setjmp 

setjmp 保存上下文环境, longjmp 使用上下文:
```
.set	noreorder
.global	__setjmp
.global	_setjmp
.global	setjmp
.type	__setjmp,@function
.type	_setjmp,@function
.type	setjmp,@function
__setjmp:
_setjmp:
setjmp:
	sd	$ra, 0($4)
	sd	$sp, 8($4)
	sd	$gp, 16($4)
	sd	$16, 24($4)
	sd	$17, 32($4)
	sd	$18, 40($4)
	sd	$19, 48($4)
	sd	$20, 56($4)
	sd	$21, 64($4)
	sd	$22, 72($4)
	sd	$23, 80($4)
	sd	$30, 88($4)
#ifndef __mips_soft_float
	sdc1	$24, 96($4)
	sdc1	$25, 104($4)
	sdc1	$26, 112($4)
	sdc1	$27, 120($4)
	sdc1	$28, 128($4)
	sdc1	$29, 136($4)
	sdc1	$30, 144($4)
	sdc1	$31, 152($4)
#endif
	jr	$ra
	li	$2, 0

.set	noreorder
.global	_longjmp
.global	longjmp
.type	_longjmp,@function
.type	longjmp,@function
_longjmp:
longjmp:
	move	$2, $5

	bne	$2, $0, 1f
	nop
	daddu	$2, $2, 1
1:
#ifndef __mips_soft_float
	ldc1	$24, 96($4)
	ldc1	$25, 104($4)
	ldc1	$26, 112($4)
	ldc1	$27, 120($4)
	ldc1	$28, 128($4)
	ldc1	$29, 136($4)
	ldc1	$30, 144($4)
	ldc1	$31, 152($4)
#endif
	ld	$ra, 0($4)
	ld	$sp, 8($4)
	ld	$gp, 16($4)
	ld	$16, 24($4)
	ld	$17, 32($4)
	ld	$18, 40($4)
	ld	$19, 48($4)
	ld	$20, 56($4)
	ld	$21, 64($4)
	ld	$22, 72($4)
	ld	$23, 80($4)
	ld	$30, 88($4)
	jr	$ra
	nop
```
