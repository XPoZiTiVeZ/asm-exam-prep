# Задача 4. Волшебная таблица

Оч. умелые хакеры обнаружили, что в таблице переходов для `switch` в коде их любимого crackme очень много пустого места, и оптимизировали её. Так как у хакеров тоже есть KPI, они просят Вас оценить их работу.

После *оптимизации* код стал выглядеть следующим образом:

```asm
section .text
h:
	dd choice.L5, choice.L1
a:
	dd choice.L3, choice.L5
c:
	dd choice.L4, choice.L2
k:
	dd choice.L3, choice.L1
u:
	db "Gradeasap", 0

global main
main:
	push ebp
	mov ebp, esp
	and esp, 0xFFFFFFF0
	call io_get_udec
	lea eax, [eax + 4 * eax]
	shr eax, 2
	sub eax, 5
	ja choice.L5
	imul eax, eax, 4
	jmp [k + eax]
choice.L2:
	lea eax, [u + 4]
	jmp choice.L7
choice.L4:
	lea eax, [u + 12 + eax]
choice.L7:
	inc eax
	jmp choice.L6
choice.L5:
	lea eax, [u]
	jmp choice.L6
choice.L1:
	lea eax, [u + 7]
	jmp choice.L6
choice.L3:
	mov eax, u
	add eax, 4
choice.L6:
	call io_print_string
	xor eax, eax
	mov esp, ebp
	pop ebp
	ret
```

Укажите ответы на следующие вопросы, каждый на отдельной строке:

Какая метка соответствует ветви `default`?  
На какую метку будет передано управление инструкцией `jmp` при вводе 4?  
Какие вводимые значения из диапазона `[0; 0xFFFF]` приведут к печати строки `asap`? Укажите все возможные варианты через пробел.  
Сколько байтов занимает таблица переходов (от первой до последней ячейки с указателями, по которым может быть передано управление)?  

## Пример форматирования ответа:

```text
choice.L7
choice.L7
100 200
333
```

<details>
<summary>Показать</summary>

```text
choice.L5
choice.L3
3
24
```
</details>