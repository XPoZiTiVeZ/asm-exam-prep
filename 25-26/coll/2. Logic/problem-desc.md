# Задача Logic: Логические операции

Для приведённого ниже фрагмента кода на языке Си напишите эквивалентный фрагмент кода на языке ассемблера.

Считайте, что переменные `i`, `x`, `y`, а также массив a уже объявлены в секции `.bss`.

Код должен состоять только из инструкций языка ассемблера и меток, реализующих выражение.

В коде **не должно** быть директив `section`, `extern`, метки `main`, инструкций `call` и `ret`.

```c
static unsigned int a[4], i, x, y;
...
y = ++x || a[i--];
```

## Ответ
<details>
<summary>Показать</summary>

```asm
    MOV dword[y], 0
    INC dword[x]
    CMP dword[x], 0
    CMOVz dword[y], 1
    Jnz .end
    
    MOV ecx, dword[i]
    CMP dword[a + ecx * 4], 0
    CMOVz dword[y], 1
    DEC dword[i]
    
    .end:
```
</details>