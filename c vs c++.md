### ✅ C vs C++
C
```c
#include <stdio.h>
int main()
{
    int a, b, max; //모든 변수 앞에 선언
    printf("Enter two integers: ");
    scanf("%d %d", &a, &b)
    return 0;
}
```
C++
```cpp
#include <iostream> // input, output 관련 라이브러리
using namespace std; 
int main(){
    int a, b; //변수 사용하기 전에만 선언되면 됨
    cout << "Enter two integers: ";
    cin >> a >> b;
    int max
    max (a > b) ? a : b;
    cout << max << endl;
    return 0;
}
```
### ✅ Function
```cpp
int Power(int base, int power) //함수가 main 함수 뒤에 있으면 앞에서 선언해줘야함, == int Power(int, int)
```
main함수와 다른 파일로 쪼개짐  
함수 안의 변수: local variable
```cpp
int n1 = 0; // global variablea
void Count()
{
    int n2 = 0; // local variable
    static int n3 = 0; // static variable: 함수 내에서만 사용 가능, 전역변수처럼 한번만 선언되고 다음에 함수를 실행해도 그 값이 저장되어있음
}
```
### ✅ Circular Buffer
```cpp
#include <iostream>
using namespace std;

// Forward = 0; Backward = 1;
enum Direction { Forward, Backward };

void CircularBuffer(Direction direction, int n) {
    const int SIZE = 8; // buffer size
    static int a[] = {0, 0, 0, 0, 1, 2, 3, 0}; // buffer
    static int front = 4, rear = 6;

    if (direction == Forward) { // insert to rear
        a[front] = 0; // modulo increment
        front = (front + 1) % SIZE;
        rear = (rear + 1) % SIZE;
        a[rear] = n;
    } else { // Backward: insert to front
        a[rear] = 0; // modulo decrement
        front = (front - 1 + SIZE) % SIZE;
        rear = (rear - 1 + SIZE) % SIZE;
        a[front] = n;
    }

    cout << "Buffer = "; // print circular buffer
    for (int i = 0; i < SIZE; i++) cout << " " << a[i];
    cout << ", front = " << front;
    cout << ", rear = " << rear << endl;
}

int main() {
    int input[] = {4, 5, 6, 7, 8, 9};
    for (int i = 0; i < 6; i++) {
        if (i < 3) 
            CircularBuffer(Forward, input[i]);
        else 
            CircularBuffer(Backward, input[i]);
    }
    return 0;
}
```
출력
>Buffer =  0 0 0 0 0 2 3 4, front = 5, rear = 7
Buffer =  5 0 0 0 0 0 3 4, front = 6, rear = 0
Buffer =  5 6 0 0 0 0 0 4, front = 7, rear = 1
Buffer =  5 0 0 0 0 0 7 4, front = 6, rear = 0
Buffer =  0 0 0 0 0 8 7 4, front = 5, rear = 7
Buffer =  0 0 0 0 9 8 7 0, front = 4, rear = 6

### ✅ Pointer
```cpp
#include <iostream>
using namespace std;

int main()
{
    const int SIZE = 5;
    int* p1 = NULL; 
    int a[SIZE] = {1, 2, 3, 4, 5}, num = 10;
    p1 = &num; // p1에 num의 메모리 주소 저장
    cout << "*p1 = " << *p1 << endl; //역참조, p1이 가리키는 주소로 가서 그곳에 저장된 실제 값 가져옴 --> 10출력

    int* p2 = NULL; // NULL = 0
    p2 = a; // p2 = &a[0];

    for (int i = 0; i < SIZE; i++) { // print array
        cout << *(p2 + i) << " "; // == p2[i]
    }

    for (int i = 0; i < SIZE; i++) { // print array
        cout << p2[i] << " ";
    }

    for (int i = 0; i < SIZE; i++, p2++) {
        cout << *p2 << " "; // print array
    }
    cout << endl;

    char s[] = "abcd"; // {'a', 'b', 'c', 'd', '\0'} --> 마지막에 null문자 포함됨
    char* p3 = s; // character pointer

    for (int i = 0; s[i] != '\0'; i++, p3++) {
        cout << *p3;
    } // print until end of string ("abcd")

    s[2] = '\0'; // {'a', 'b', '\0', 'd', '\0'}
    cout << " " << s; // "ab"

    return 0;
}
```
출력값
>*p1 = 10  
1 2 3 4 5 1 2 3 4 5 1 2 3 4 5   
abcd ab

### ✅ Structure
```cpp
struct Node{
    Data data;
    Node* next;
}
```
public으로 정의되는거 빼면 클래스와 같음  
함수도 넣을 수 있음