# Задача 5. Выражения

Выберите из приведенных фрагментов ассемблерного кода возможные реализации выражения.

Правильные варианты ответа для каждого выражения выпишите подряд без пробелов в алфавитном порядке. Ответ для каждого выражения начинайте с новой строки. Если ни один из вариантов не подходит, оставьте строку пустой.

**1.**

```c
unsigned short *p;

*p %= 16
```

```asm
section .bss

  p resd 1
```

|A|B|C|D|
|:-|:-|:-|:-|
|mov ax, word [p]|mov eax, dword [p]|mov edi, dword [p]|mov edi, dword [p]|
|mov cx, 0x10|mov dx, word [eax]|mov ax, word [edi]|mov ax, word [edi]|
|xor dx, dx|and dx, 0xF|mov cx, 0x10|mov cx, 0x10|
|div cx|mov word [eax], dx|cwd|xor edx, edx|
|mov word [p], dx||idiv cx|div cx|
|||mov word [edi], dx|mov word [edi], ax|

**2.**

```c
unsigned short a, b, c;

c = (a | b) >> 8
```

```asm
section .bss
    a resw 1
    b resw 1
    c resw 1
```


|A|B|C|D|
|:-|:-|:-|:-|
|mov ax, word [a]|mov ax, word [a]|mov ax, word [a]|movzx eax, word [a]
|or ax, word [b]|mov dx, word [b]|or ax, word [b]|movzx edx, word [b]
|shr ax, 8|mov cl, ah|rol ax, 8|xor eax, edx|sal eax, 8
|mov word [c], ax|xor cl, dh|movzx word [c], al|movzx word [c], al
||movzx word [c], cl|
|


## Пример правильно форматированного ответа:

```text
AD
B
```

## Ответ
<details>
<summary>Показать</summary>

```text
B
A
```
</details>