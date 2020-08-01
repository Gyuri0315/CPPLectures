# 함수 오버로드(함수 중복)의 원칙

C++에서 다음 함수의 정의는 오버로드할 수 없다.

* 반환 자료형만 다른 같은 이름의 함수 선언

다음 코드의 ```func```두 함수는 반환 자료형만 다르기 떄문에 ```main``` 함수에서 ```func``` 함수 호출 시 첫 번째 함수를 실행하여야 하는지 두 번째 함수를 실행하여야 하는지 결정할 수 없기 때문에 함수 오버로딩을 할 수 없다.  

```cpp
int func() {
	return 100;
}

char func() {
	return 'k';
}

int main(int argc, char const *argv[]){
	char x = func();
	return 0;
}
```

* 디폴트 인자가 설졍된 함수 선언

아래의 코드의 ```sum``` 함수는 입력 인자의 개수가 각각 두 개, 세 개로 정의되어 있다. 
그러나 두 번째 함수에는 디폴트 안자가 있어 두 번째 함수를 호출할 때 인자를 두 개만 전달하여도 함수 호출이 가능하다. 
아래의 코드의 ```main```함수에서 ```sum```함수 호출이 두 번 있다. 
첫 번쨰 ```sum```  함수 호출 시 입력 인자로 세 개의 정수 값이 전달되었기 때문에 두 번째로 정의된 함수를 호출하게 된다.
두 번째 ```sum```함수 호출 시 입력 인자로 두 개의 정수 값이 전달되는데 이 때 첫 번쨰 함수를 실행하여야 하는지 두번 째 함수를 실행하여야 하는지 결정할 수 없기 떄문에 에러가 발생한다. 

그러므로 **디폴트 인자**가 있는 경우 함수 오버로딩을 주의하여야 한다. 

  * ```sum(10, 20, 30);```
  * ```sum(10, 20);```

```cpp
int sum(int a, int b) {
	return a + b;
}

int sum(int a, int b, int c = 100) {
	return a + b + c;
}

int main(int argc, char const *argv[])
{
	int result = sum(10, 20, 30);  // 세개의 파러미터
	result = sum(10, 20);          // 컴파일 에러를 발생시키는 코드 
	cout << "result: " << result << endl;
	return 0;
}
```

* 다음의 두 함수는 인자의 모습이 다를 뿐 의미가 같기 때문에 오버로딩되지 않는다.

	- ```int func(int* buf);```
	- ```int func(int buf[]);```

* 다음의 ```static``` 함수와 일반 함수도 오버로딩되지 않는다.

	- ```static int func();```
	- ```int func();```

* 다음의 경우도 두 함수는 오버로딩 되지 않는다.

	- ```int func(int x);```
	- ```int func(const int x)```

