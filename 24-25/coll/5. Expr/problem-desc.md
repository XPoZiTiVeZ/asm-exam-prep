# Задача Expr: Выражения

Выберите из приведенных фрагментов ассемблерного кода возможные реализации выражения.

Правильные варианты ответа для каждого выражения выпишите подряд без пробелов в алфавитном порядке. Ответ для каждого выражения начинайте с новой строки. Если ни один из вариантов не подходит, оставьте строку пустой.

## 1.

```c
short a[5][7], x;
x = (*a[3] > 0) - (*a[3] < 0);
```

```asm
section .bss
  a resw 35
  x resw 1
```

|A|B|C|D|
|:--|:--|:--|:--|
|xor dx, dx|xor dx, dx|xor dx, dx|xor dx, dx|
|mov eax, dword [a]|mov di, 1|mov ax, word [a + 3*7*2]|mov cx, -1|
|mov ax, word [eax + 3*7*2]|mov si, -1|test ax, ax|mov eax, dword [a]|
|test ax, ax|mov ax, word [a + 3*5*2]|setg dl|mov eax, dword [eax]|
|setg dl|cmp ax, 0|shr ax, 15|cmp word [eax + 3*2], 0|
|mov word [x], dx|cmovg dx, di|sub dx, ax|setg dl|
|setl dl|cmovl dx, si|mov word [x], dx|cmovl dx, cx|
|sub word [x], dx|mov word [x], dx||mov word [x], dx|
|||||


## 2.

```c
unsigned short x;
x = (x >> 4) | (x << 12);
```

```asm
section .bss
  x resw 1
```

|A|B|C|D|
|:-|:-|:-|:-|
|rol word [x], 12|ror word [x], 4|rol word [x], 4|mov dx, word [x]|
|||ror word [x], 12|mov cx, dx|
||||sar dx, 4|
||||sal cx, 12|
||||or dx, cx|
||||mov word [x], cx|
|||||


## 3.

```c
unsigned char p[16], *q, c;
c = p[4] || q[1];
```

```asm
section .bss
  p resb 16
  q resd 1
  c resb 1
```

|A|B|C|D|
|:-|:-|:-|:-|
|mov al, byte [p + 4]|mov dl, 1|xor dl, dl|mov dl, 1|
|test al, al|cmp byte [p + 4], 0|mov cl, 1|mov al, byte [p + 4]|
|setnz dl|jnz .nz|cmp byte [p + 4], 0|and al, al|
|mov al, byte [q + 1]|cmp byte [q + 1], 0|cmovnz dl, cl|jnz .nz|
|setnz cl|setnz dl|mov byte [c], dl|mov eax, dword [q]|
|or dl, cl|.nz:|mov eax, dword [q]|cmp byte [eax + 1], 0|
|mov dword [c], dl|mov byte [c], dl|cmp byte [eax + 1], 0|setnz dl|
|||cmovnz dl, cl|.nz:|
|||or byte [c], dl|mov byte [c], dl|
|||||

## Пример правильно форматированного ответа:

```text
A
CD
ABCD
```

## Ответ
<details>
<summary>Показать</summary>

```text
C
AB
D
```
</details>