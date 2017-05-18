## Reversing this [source file](crackme30)

> Mở file bằng IDA Pro ta có được đoạn code `C` như sau:

```C
signed __int64 __fastcall main(int a1, char **a2, char **a3)
{
  const char *v3; // rdi@2
  char *v4; // rdx@3
  signed __int64 v5; // rcx@3
  char *v6; // rdi@3
  bool v7; // zf@5
  _BYTE *v8; // rcx@7
  int v9; // eax@7

  if ( a1 == 2 )
  {
    v4 = a2[1];
    v5 = -1LL;
    v6 = a2[1];
    do
    {
      if ( !v5 )
        break;
      v7 = *v6++ == 0;
      --v5;
    }
    while ( !v7 );
    if ( v5 == -10 )
    {
      v8 = &unk_400808;
      v9 = 0;
      while ( (v9 ^ *v4) == *v8 )
      {
        v9 += 10;
        ++v4;
        ++v8;
        if ( v9 == 80 )
        {
          puts("OK");
          return 0LL;
        }
      }
    }
    v3 = "KO";
  }
  else
  {
    v3 = "Usage: ./crackme password";
  }
  puts(v3);
  return 1LL;
}
```
Sử dụng `Hexview` ta có nội dung của biến `unk_400808` là: `67 39 66 2E 46 03 51 76  01 1B 03 3B 2C 00`

```py
a = '67 39 66 2E 46 03 51 76  01 1B 03 3B 2C'
a = a.replace(' ','')
a = a.decode('hex')
rs = ''
v9 = 0
for x in a:
    rs += chr(ord(x)^v9)
    v9 += 10

print rs
```
Từ đó ta có kết quả là : `g3r0n1m0QAgUT`
