## Compiler this [source file](RE10.jar)

> Sử dụng tool online [Online Tool](http://www.javadecompilers.com/)

Ta có được đoạn code sau:

```java
import java.io.PrintStream;

public class Main
{
  public Main() {}
  
  public static void main(String[] paramArrayOfString) {
    int[] arrayOfInt1 = { 229, 102, 166, 229, 227, 205, 80, 224, 122, 168, 56, 185, 1, 154, 43, 127, 139, 83, 211, 202, 240 };
    int[] arrayOfInt2 = { 212, 7, 249, 175, 162, 155, 49, 191, 62, 247, 90, 214, 108, 248, 116, 62, 255, 60, 190, 163, 155 };
    int i = 1;
    if (paramArrayOfString.length == 0) {
      System.out.println("Usage: ./crackme password");

    }
    else if (paramArrayOfString[0].length() != arrayOfInt1.length) {
      System.out.println("Wrong!");
    }
    else {
      int j = 0;
      while (j < arrayOfInt1.length) {
        if ((paramArrayOfString[0].charAt(j) ^ arrayOfInt1[j]) != arrayOfInt2[j]) {
          i = 0;
        }
        j++;
      }
      if (i != 0) {
        System.out.println("Success!");
      }
      else {
        System.out.println("Wrong!");
      }
    }
  }
}
```

> Từ đó dễ dàng tính ra được kết quả `1a_JAVa_D_bomb_Atomik`

```py
arrayOfInt1 = [ 229, 102, 166, 229, 227, 205, 80, 224, 122, 168, 56, 185, 1, 154, 43, 127, 139, 83, 211, 202, 240 ]
arrayOfInt2 = [ 212, 7, 249, 175, 162, 155, 49, 191, 62, 247, 90, 214, 108, 248, 116, 62, 255, 60, 190, 163, 155 ]
rs = ''
for i in range(len(arrayOfInt1)):
    rs += chr(arrayOfInt1[i]^arrayOfInt2[i])

print rs
```
