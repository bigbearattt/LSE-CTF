## Reversing this [source file](crackme80)

> File này là file `LLVM IR bitcode`

> Sử dụng `llc` để compile từ bitcode qua assembly.

> `$ llc -O3 crackme80 -o crackme80.s`

> `$ gcc crackme80 -o crackme`

> Sử dụng IDA pro để đọc file `crackme` [source file](crackme) ta có:

```C
int __cdecl main(int argc, const char **argv, const char **envp)
{
  const char *v3; // rdi@10
  char *dest; // [sp+20h] [bp-30h]@3
  unsigned int v6; // [sp+2Ch] [bp-24h]@3
  int v7; // [sp+30h] [bp-20h]@3
  int v8; // [sp+34h] [bp-1Ch]@2
  signed int v9; // [sp+38h] [bp-18h]@3
  signed int v10; // [sp+3Ch] [bp-14h]@3
  int i; // [sp+40h] [bp-10h]@3
  signed int j; // [sp+44h] [bp-Ch]@6

  if ( argc == 2 )
  {
    v6 = strlen("^Hå¦¢-Ä\bt\rvÿ+,¼mÜ|e\x1B\n8ßç`¦:¦+\n¦<");
    v9 = strlen(argv[1]);
    v10 = v9 - v9 % 8 + 8;
    v7 = v6 != v9;
    dest = (char *)malloc(v10);
    memset(dest, 0, v10);
    strncpy(dest, argv[1], v9);
    for ( i = 0; i < v10 / 8; ++i )
      proces((__int64)&dest[8 * i], (__int64)"PFpuQVgKNFCvpqA4");
    for ( j = 0; j < (signed int)check(v6, v9); ++j )
      v7 |= aHjIOCVsMmU8sz[j] != dest[j];
    free(dest);
    if ( v7 )
      v3 = "Wrong password.\n";
    else
      v3 = "Good password, well played :)\n";
    printf(v3, (unsigned int)v9, "PFpuQVgKNFCvpqA4");
    v8 = 0;
  }
  else
  {
    ____________(*argv, argv, envp);
    v8 = 1;
  }
  return v8;
}
```
> Hàm con sử lý xâu:
```C
__int64 __fastcall proces(__int64 a1, __int64 a2)
{
  __int64 result; // rax@4
  unsigned int i; // [sp+24h] [bp-10h]@1
  unsigned int v4; // [sp+28h] [bp-Ch]@1
  unsigned int v5; // [sp+2Ch] [bp-8h]@1
  int v6; // [sp+30h] [bp-4h]@1

  v4 = *(_DWORD *)a1;
  v5 = *(_DWORD *)(a1 + 4);
  v6 = 0;
  for ( i = 0; i <= 31; ++i )
  {
    v6 -= 0x61C88647;
    v4 += (*(_DWORD *)a2 + 16 * v5) ^ (v5 + v6) ^ (*(_DWORD *)(a2 + 4) + (v5 >> 5));
    v5 += (*(_DWORD *)(a2 + 8) + 16 * v4) ^ (v4 + v6) ^ (*(_DWORD *)(a2 + 12) + (v4 >> 5));
  }
  *(_DWORD *)a1 = v4;
  result = v5;
  *(_DWORD *)(a1 + 4) = v5;
  return result;
}
```
> Và:
```C
__int64 __fastcall ___________(unsigned int a1, unsigned int a2)
{
  __int64 result; // rax@2

  if ( (signed int)a1 >= (signed int)a2 )
    result = a2;
  else
    result = a1;
  return result;
}
```
> Ta có lời giải sau:
```C
#include <stdio.h>
#include <string.h>

void process(char *a1, char *a2){
	unsigned int v4 = *(int*)a1;
	unsigned int v5 = *(int*)(a1+4);
	int v6 = 0xc6ef3720;
	int i;
	for (i = 0; i <= 31; i++){
		v5 -= (*(unsigned int*)(a2 + 8) + 16 * v4) ^ (v4 + v6) ^ (*(unsigned int*)(a2 + 12) + (v4 >> 5));
		v4 -= (*(unsigned int*)a2 + 16 * v5) ^ (v5 + v6) ^ (*(unsigned int*)(a2 + 4) + (v5 >> 5));
		v6 += 0x61C88647;
	//	printf("%d\n",v6);
	}
	char a[9];
	memcpy(a,&v4,4);
	memcpy(a+4,&v5,4);
	a[8]=0;
	printf("%s",a);
}

int main(){
	char *buf = "PFpuQVgKNFCvpqA4";
	char *dest = "\x5E\x48\x86\xB2\x9B\xCB\x8E\x08\xE7\x0D\x76\x98\xD7\x2C\xAC\x6D\x9A\x7C\xEE\x1B\x0A\x38\xE1\x87\x60\xBA\x3A\xDD\xBD\x0A\xB6\x3C\x00";
	int i;
	for (i=0; i<4; i++){
		process(dest+8*i, "PFpuQVgKNFCvpqA4");
	}
}
```
> Ta được kết quả là: `flag{llvM_1R_1s_b3TT3r_th4n_4SM}`
