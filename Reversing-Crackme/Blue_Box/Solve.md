## Reversing this [source file](re30)

> Mở file bằng IDA pro ta có:

```C
int __cdecl main(int a1, char **a2)
{
  size_t v2; // eax@2
  int result; // eax@2
  signed int v4; // [sp+10h] [bp-30h]@1
  signed int v5; // [sp+14h] [bp-2Ch]@1
  signed int v6; // [sp+18h] [bp-28h]@1
  signed int v7; // [sp+1Ch] [bp-24h]@1
  signed int v8; // [sp+20h] [bp-20h]@1
  signed int v9; // [sp+24h] [bp-1Ch]@1
  signed int v10; // [sp+28h] [bp-18h]@1
  int (*v11)(); // [sp+2Ch] [bp-14h]@1
  signed int v12; // [sp+30h] [bp-10h]@1
  int v13; // [sp+34h] [bp-Ch]@5
  signed __int32 v14; // [sp+38h] [bp-8h]@5
  signed __int32 v15; // [sp+3Ch] [bp-4h]@3

  v11 = sub_8048550;
  v12 = 0;
  v4 = 1734439765;
  v5 = 540680293;
  v6 = 1919102766;
  v7 = 1835754337;
  v8 = 1634738277;
  v9 = 1870099315;
  v10 = 681074;
  if ( a1 == 2 )
  {
    v15 = strlen(a2[1]);
    if ( v15 == 21 )
    {
      v14 = 0;
      v13 = 0;
      while ( v14 < v15 )
      {
        if ( *((_BYTE *)v11 + v14) && *((_BYTE *)v11 + v14) != -1 )
        {
          if ( *((_BYTE *)v11 + v14) != ((unsigned __int8)a2[1][v13] ^ *(_BYTE *)(v13 + 0x8049B90)) )
          {
            v12 = 1;
            break;
          }
          ++v13;
        }
        else
        {
          ++v15;
        }
        ++v14;
      }
      if ( v12 )
      {
        write(1, "Next time!\n", 0xBu);
        result = 0;
      }
      else
      {
        write(1, "Congrats!\n", 0xAu);
        result = 1;
      }
    }
    else
    {
      write(1, "Next time!\n", 0xBu);
      result = 0;
    }
  }
  else
  {
    v2 = strlen((const char *)&v4);
    write(1, &v4, v2);
    result = 0;
  }
  return result;
}
```

> Sử dụng Hexview để xem nội dung của biến có địa chỉ `8049B90` là : `34 D6 A8 E2 88 77 AA 04  9E 98 33 82 DA 54 8F 1B 45 5B 37 BB 1D 00`
> Giá trị được trỏ bởi biến `v11` là : 
```
55 89 E5 83 EC 28 C7 45  F0 00 00 00 00 C7 45 F4 
00 00 00 00 EB 20 C7 44  24 04 01 00 00 00 8B 45 
F4 89 04 24 E8 A7 FE FF  FF 83 F8 FF 74 04 83 45
```
```py
a = "55 89 E5 83 EC 28 C7 45  F0 00 00 00 00 C7 45 F4 00 00 00 00 EB 20 C7 44  24 04 01 00 00 00 8B 45 F4 89 04 24 E8 A7 FE FF  FF 83 F8 FF 74 04 83 45"
b = "34 D6 A8 E2 88 77 AA 04  9E 98 33 82 DA 54 8F 1B 45 5B 37 BB 1D"
b = b.replace(' ','')
a = a.replace('00','')
a = a.replace('FF','')
a = a.replace(' ','')

a = a.decode('hex')
b = b.decode('hex')
rs = ''
for i in range(len(b)):
    rs += chr(ord(b[i])^ord(a[i]))

print rs
```
> Chạy đoạn code trên ta có đáp án: `a_Mad_mAn_vv1tH_a_60X`
