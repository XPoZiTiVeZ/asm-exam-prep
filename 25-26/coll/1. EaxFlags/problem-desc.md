# Задача EaxFlags: Определение значения регистра EAX и флагов

Секция `.data` была размещена в памяти, начиная с базового адреса `0x0804ea34`. Укажите значение регистра EAX и флагов после выполнения указанных команд секции `.text`.

```asm
section .data
    a dw 0x2021, 0x2023, 0x2025
    s db "september", 0
    b dd 0xBEFECECD
    p dd b

section .text
    movsx eax, word[b + 1] ; (1)
    add al, byte[p]        ; (2)
    movzx ax, byte[a + 4]  ; (3)
```

Скопируйте 3 строки ниже в поле ответа и заполните прочерки значениями регистра EAX (в шестнадцатеричном виде) и флагов (0/1) после выполнения соответствующих инструкций:

```text
(1) EAX = -
(2) EAX = -, CF = -, OF = -, ZF = -, SF = -
(3) EAX = -
```

## Пример возможного формата ответа:

```text
(1) EAX = 0xcafebabe
(2) EAX = 0x00000000, CF = 0, OF = 0, ZF = 1, SF = 0
(3) EAX = 0x00cafeba
```

## Ответ
<details>
<summary>Показать</summary>

```text
(1) EAX = 0xfffffece
(2) EAX = 0xfffffe06, CF = 1, OF = 0, ZF = 0, SF = 0
(3) EAX = 0xffff0025
```
</details>