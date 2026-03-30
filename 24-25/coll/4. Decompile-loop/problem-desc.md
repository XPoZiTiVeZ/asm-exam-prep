# Задача Decompile: Декомпиляция программы с циклом

Дан фрагмент кода на языке Си c тремя пропусками:

```c
#define N 1024

int s[N], t[N], g[N];
int x;
...
for (int i = 0; пропуск_1) {
    пропуск_2 ;
    пропуск_3 ;
}
```

Для этого фрагмента (после ...) компилятор построил следующий код:

```asm
    mov     ebx, dword[x]
    mov     esi, 3
    dec     ebx
    xor     ecx, ecx
.S:
    cmp     ecx, ebx
    jnl     .F
    mov     eax, dword[t + ecx*4]
    cdq
    idiv    esi
    mov     eax, dword[t + ecx*4]
    mov     edi, eax
    xor     edi, 2
    cmp     edx, 0
    cmovne  eax, edi
    mov     dword[s + ecx*4 + 4], eax
    mov     eax, dword[s + ecx*4]
    imul    dword[g + ecx*4], eax
    inc     ecx
    jmp     .S
.F:
```

Вам необходимо восстановить пропуски в исходном фрагменте кода на языке Си. Выпишите их в ответе по одному на строке. В ответе должно быть ровно три строки. Если не получается заполнить какой-то из пропусков, оставьте эту строку пустой.

**Внимание**: запрещено менять переменную `i` во 2-м и 3-м пропусках.

## Пример форматирования ответа:

```text
i<=5; i*=2
x = 3
x += 7
```

## Ответ
<details>
<summary>Показать</summary>

```text
i >= x; i++
s[i + i] = t[i] % 3 == 0 ? t[i] : t[i] ^ 2
g[i] *= s[i]
```
</details>