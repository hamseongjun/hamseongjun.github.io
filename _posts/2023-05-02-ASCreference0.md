---
layout: single
title: "참고용 : 리눅스, C언어 치트시트"
categories: "ASC-Programing_study"
tags: [ASC, 참고용]
author_profile: false
sidebar:
    nav: "counts"
---

<br>

# 참고용 : 리눅스, C언어 치트시트

## 리눅스 CheetSheet

- pwd : 현재 위치 출력
- ls : 디렉토리의 파일, 폴더 등 출력
    - -a : 숨김 파일들도 출력
    - -l : 자세히 보기
- cd : 디렉토리 이동
    - . : 현재 디렉토리
    - .. : 상위 디렉토리
    - ~ : 홈 디렉토리
    - / : 최상위 경로
- mkdir dir : 폴더 생성
- mv source1 [source2 ..] dir : source(s) dir위치로 이동
- mv source1 source2 : source1 파일명 source2로 변경
- cp [options] source1 source2 : source1 source2로 복사
    - -R : 하위 디렉토리 내용도 복사
- rm source : source 삭제
    - -f : 강제로 삭제
    - -r : 디렉토리 내부도 삭제
    - -d : 비어있는 디렉토리 삭제
- cat source : source 파일 내용 출력
- head source : 상위 10줄 출력
- tail source : 하위 10줄 출력
- man cmd : cmd에 대한 메뉴얼(명령어, 시스템 콜)
- history : 사용했던 명령어 리스트
- gcc -o filename, filename.c : gcc 컴파일
    - -c : Object file 생성

## C언어 CheetSheet

```c
/* 여러라인 주석*/
// 한줄 주석

#include <system-header.h>
#include "user-header.h"

#define symbol replacement-text

// .h files: #defines, typedefs, function prototypes
// .c files: #defines, structs, statics, function definitions;

int main (int argc , char *argv [])

// 식별자는 문자로 시작하고 그 뒤에 문자, 숫자 또는 밑줄이 옵니다

// reserved (예약어)
/* auto break case char const continue default do double else enum extern float for goto if inline int long register restrict return short signed sizeof static struct switch typedef union unsigned void volatile while Bool Complex Imaginary
*/

// Statements
if (condition) statement [ else statement]
while (condition) statement
return [value]; return (optional) value from function

// Operators
x++ : 증가 연산자(뒤, 후위)
x-- : 감소 연산자(뒤, 후위)
( ) : 함수 호출 or 우선 연산
[ ] : 배열 첨자
. : 구조체/공용체 멤버 접근
-> : 포인터로 구조체/공용체 멤버 접근
(자료형){값} : 복합 리터럴

++x : 증가 연산자(앞, 전위)
--x : 감소 연산자(앞, 전위)
+x : 단항 덧셈(양의 부호)
-x : 단항 뺄셈(음의 부호)
! : 논리 NOT
~ : 비트 NOT
(자료형) : 자료형 캐스팅(변환)
*x : 포인터 x 역참조
&x : x의 주소
sizeof : 크기

*, /, % : 곱셈, 나눗셈, 나머지
+,- : 덧셈, 뺄쌤
<<, >> : 비트 왼쪽,오른쪽으로 쉬프트

<, <=, >, >=, ==, != : 비교
& : 비트 AND
^ : 비트 XOR
| : 비트 OR
&& : 논리 AND
|| : 논리 OR
? : : 삼항 연산자
=, +=, -=, *=, /=, %=, <<=, >>=, &=, ^=, |= : 할당 연산
 

Literals
integers (int): 123 -4 0xAf0C 057
reals (double): 3.14159265 1.29e-23
characters (char): 'x' 't' '\033'
strings (char *): "hello"  "abc\"\n" ""

Decalrations
int i , length ;
char *str , buf [BUFSIZ], prev ;
double x , values [MAX];
typedef enum { FALSE, TRUE } Bool;
typedef struct { char *key ; int val ; } keyval t;

Initialisation
int c = 0;
char prev = '\n';
char *msg = "hello";
int seq [MAX] = { 1, 2, 3 };
keyval t keylist [] = {
”NSW”, 0, ”Vic”, 5, ”Qld”, -1 };

Character & String Escapes
\n line feed (“newline”) 
\r carriage return 
\t horizontal tab 
\e escape 
\' single quote 
\" double quote 
\\ backslash
\0 null character
\ddd octal ascii value
\xdd hex ascii value

// in stdlib.h
#define NULL ((void *)0)
void *malloc (size t size );
void *calloc (size t number , size t size );
void free (void *obj );
void exit (int status ); void abort ();
int atoi (char *str );
long strtol (char *str , char **end , int base );
double atof (char *str );
int abs (int x );

// in string.h
size t strlen (char *str ); // the length of str without trailing nul.
char *strcpy (char *dst , char *src );
size t strlcpy (char *dst , char *src , size t sz );
char *strcat (char *dst , char *src );
int strcmp (char *s1, char *s2); /// return < 0, = 0, > 0 if s1 <, =, > s2
char *strchr (char *str , int c );
char *strrchr (char *str , int c );
char *strstr (char *haystack , char *needle );
char *strpbrk (char *str , char *any );
size t strspn (char *str , char *any );
size t strcspn (char *str , char *any );
char *strsep (char **strp , char *sep );

 
// in ctype.h
int toupper (int c ); int tolower (int c );
int isupper (int c ); int islower (int c );
int isalpha (int c ); int isalnum (int c );
int isdigit (int c ); int isxdigit (int c );
int isspace (int c ); int isprint (int c );

// in math.h
// compile and link -lm if not using dcc
double sin (double x ); 
double asin (double x );
double cos (double x );
double acos (double x );
double tan (double x );
double atan (double x );
double atan2 (double y , double x );
double exp (double x );
double log (double x );
double log10 (double x );
double pow (double x , double y );
double sqrt (double x );
double floor (double x ); double ceil (double x );
double fabs (double x );
double fmod (double x , double y );

// in stdio.h
#define EOF (-1)
FILE *stdin , *stdout , *stderr ;
FILE *fopen (char *filename , char *mode );
int fclose (FILE *fh );
int fgetc (FILE *fh );
int getchar (void);
char *fgets (char *s , int size , FILE *fh );
int fputc (int c , FILE *fh );
int putchar (int c );
putchar (k) equivalent to fputc (k, stdout )
int fputs (char *str , FILE *fh );
int puts (char *str );
int printf (char *fmt , ...);
int fprintf (FILE *fh , char *fmt , ...);
int sprintf (char *str , char *fmt , ...);
int scanf (char *fmt , ...);
int fscanf (FILE *fh , char *fmt , ...);
int sscanf (char *str , char *fmt , ...);
```

## ASCII Table
![](https://velog.velcdn.com/images/hamseongjun/post/a120cc40-ca85-4885-acc0-49defe1d9a95/image.png)

