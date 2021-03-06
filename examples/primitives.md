# Java is weird.

## Primitives

#### Divide by zero

```java
double a = 1. / 0;    // Infinity
float  b = 1f / 0;    // Infinity
int    c = 1  / 0;    // (ArithmeticException)
short  d = 1; d /= 0; // (ArithmeticException)
byte   e = 1; e /= 0; // (ArithmeticException)
```

#### Mod

```java
int a =  0 % 10;  // 0
int b = 10 % 0;   // 0 (ArithmeticException)
int c = 10 % 10;  // 0
int d = -1 % 10;  // -1
int e =  1 % -10; // 1
int f = -1 % -10; // -1
int g = -1 % -10; // -1
```

#### Casting

```java
byte a = Byte.MAX_VALUE;       // 127
a + 3;                         // 130

int b = Integer.MAX_VALUE;     // 2147483647
b + 1.;                        // 2.147483648E9

int c = 1.5;                   // (Compile Error)
int d = 0; d += 1.5;           // 1

byte e = 127;                  // 127
byte f = 128;                  // (Compile Error, lossy)
byte g = 'z';                  // 122 (ascii of z)
byte h = 'Ç';                  // (Compile Error, lossy)

short i = Short.MAX_VALUE - 1; // (Valid)
short j = Short.MAX_VALUE + 1; // (Compile Error, lossy)
```

#### Shifting

```java
double a = 1; a <<= 2; // (Compile Error)
float  b = 1; b <<= 2; // (Compile Error)
int    c = 1; c <<= 2; // 4
short  d = 1; d <<= 2; // 4
byte   e = 1; e <<= 2; // 4

int  f = 5; f <<= 32;   // 5 (actually x << (32 % INT_SIZE))
int  g = 5; g <<= 64;   // 5
byte h = 5; h <<= 8;    // 0
byte i = 5; i <<= 32;   // 5
```

#### Bitwise Complement Operator

```java
double a = 7; ~a; // (Compile Error)
float  b = 7; ~b; // (Compile Error)
int    c = 7; ~c; // -8
short  d = 7; ~d; // -8
byte   e = 7; ~e; // -8
```

#### Infinity

```java
double a = 1. / 0; // Infinity
a * -1;            // -Infinity
a / 2;             // Infinity
a - 5;             // Infinity
a / a;             // NaN
a - a;             // NaN
```

#### Lack of precision

```java
double a = 1e30;
double b = a + 10;
a == b; // true
```

#### Zero

```java
-0 == 0; // true
```

#### Objects

```java
5 == 5;                           // true
new Integer(5) == 5;              // true

Integer a = 5;
Integer b = 5;
Integer c = new Integer(5);
Integer d = new Integer(5);
a == b;                           // true
c == d;                           // false
c == a;                           // false

Integer e = 128;
Integer f = 128;
e <= f;                           // true
e >= f;                           // true
e == f;                           // false
```

#### Ternary

```java
int    a = true ? 1 : 1.0;    // (Compile Error)
Object b = true ? 1 : 2.5;    // 1.0

Integer c = null;
double  d = 2.0;
Object  e = true ? null : d;  // null
Object  f = true ?    c : d;  // (NullPointerException)
```

#### Literals

```java
int a = 05;        // 5
int b = 010;       // 8
int c = 08;        // (Compile Error)

int d =  x10;      // (Compile Error)
int e = 0x10;      // 16

int f = 0b1111;    // 15
int g = 0b10;      // 2
int h = 0b12;      // (Compile Error)

int    i = 1e2;    // (Compile Error)
double j = 1e2;    // 100.0

int k = 1_22_3;    // 1223
int l = 1_22_;     // (Compile Error)
int m = _22_3;     // (Compile Error)
double n = 3.1_4;  // 3.14
int o = 0_10;      // 8
int p = 0b_10;     // (Compile Error)
long q = 1_0L;     // 10
long r = 10_L;     // (Compile Error)

double s = 1.0d;   // 1.0
double t = 1d;     // 1.0
```

#### Increment/Decrement

```java
int a = 3;
a++;          // 3
a;            // 4

int b = 3;
++b;          // 4
b;            // 4

int c = 3;
c += c += 1;  // (left hand value preserved during evaluation)
c;            // 7
```

#### Valid Arithmetic

```java
Character a = 'a';
a++;               // (Valid)
a += 1;            // (Compile Error, incompatible types)
a += 'z';          // (Compile Error, incompatible types)

char b = 'a';
b++;               // (Valid)
b += 1;            // (Valid)
b += 'z';          // (Valid)

Double c = 3.14;
c++;               // (Valid)
c += 1;            // (Valid)
c += 2.2;          // (Valid)
```