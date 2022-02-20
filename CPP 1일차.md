# CPP 1일차

## CPP를 하기로 결정한 이유

다양한 자료구조와 알고리즘을 모르는 상황에서 파이썬 내장 함수를 이용하여 문제를 풀려고 하니 (예를 들자면 큰 수 정렬 등) 시간초과나 메모리 초과가 빈번하게 일어났고, PS에서 많이 쓰이는 cpp를 배우는 게 앞으로의 공부에 있어서 더 좋다고 생각했다.

백준 특정 문제를 검색했을 때 cpp 검색 결과가 파이썬에 비해 확연히 많이 나오는 것도 장점이다. 추가로 SDK나, IDE를 설치할 필요없이 Xcode에서 바로 코딩이 가능하다는 것도 장점이다.

## cpp 입출력

입출력이 생각보다 간단하다. 맨 위에 `using namespace std`를 선언하면 `std::cin >> a` 대신 `cin >> a`라는 코드로 좀 더 간결하게 입출력을 할 수 있다. 글로벌로 선언하니 저걸 쓰지 말라느니 검색해보면 복잡한데 입출력하는 지금 단계에서 고민할만한 문제는 아닌 것 같다.

scanf나 printf도 쓸 수 있는 것 같은데 굳이 쓸 필요는 없고...

백준 1000번 A+B 문제 소스 코드다. a, b 변수 두 개 선언하고 두 변수 차례대로 입력받고 두 개 더한 값 출력하고 `endl`로 개행해주고 리턴하면 끝이다. Rust면 모르겠는데 이건 하나도 안 복잡함

```cpp
#include <iostream>
using namespace std;

int main() {
    int a, b;
    cin >> a >> b;
    cout << a + b << endl;
    return 0;
}
```

## 구구단

대충 아래처럼 하면 되는 것 같다. 어째 파이썬보다 쉬워보인다.  반복문은 흔히 아는 for문으로도 되고 while문으로도 된다 하고, 조건문도 그냥 if다. 어려울 게 없다.

```cpp
#include <iostream>
using namespace std;

int main() {
    int a, i;
    cin >> a;
    
    for (i = 1; i <= 9; i ++) {
        cout << a << " x " << i << " = " << a * i << endl;
    }
    
    return 0;
}
```

## split 함수가 없다?

아니 이게 없으면 문제를 어떻게 풀라는 거지 따로 함수를 만들어가지고 써야 된다고 한다. JS랑 파이썬 하던 사람한테는 낭패가 따로 없다. 뭐 정렬 함수도 없는데 split이 있는 게 더 신기하긴 하지...

아래처럼 하는 건 stringsteam을 사용한 split이라고 한다. 정말 길다. `"lee-ha-ram"` 이거 하나 split하는데 30줄 정도가 필요하다. 

```cpp
#include <iostream>
#include <vector>
#include <sstream>

using namespace std;
vector<string> split(string str, char delimiter);

int main() {
    string test = "lee-ha-ram";
    vector<string> result = split(test, '-');
    
    for (int i = 0; i < result.size(); i ++){
        cout << result[i] << " ";
    }
    
    cout << endl;
    return 0;
}

vector<string> split(string input, char delimiter) {
    vector<string> answer;
    stringstream ss(input);
    string temp;
 
    while (getline(ss, temp, delimiter)) {
        answer.push_back(temp);
    }
 
    return answer;
}
```

아래처럼 하면 조금 더 직관적이고 짧다. 똑같이 vector와 sstream을 사용한 방법이긴 하다.

```cpp
#include<iostream>
#include<string>
#include<vector>
#include<sstream>

using namespace std;

int main()
{
    string str = "lee-ha-ram";
    
    istringstream ss(str);
    string stringBuffer;
    vector<string> x;
    x.clear();

    while (getline(ss, stringBuffer, '-')){
        x.push_back(stringBuffer);
        cout << stringBuffer << " ";
    }
    
    cout << endl;
    
    return 0;
}
```

## vector가 뭘까

Rust 하는 놈한테 많이 듣긴 했는데 내가 아는 벡터라곤 배그에 나오는 것밖에 없다.

array와 비슷한 기능을 하는 배열이라고 한다. 그런데 array는 딱 크기를 정해버리면 방 크기를 더 못 늘리는데 벡터는 그냥 슉.슈슉 늘릴 수 있다고 한다. 좀 멋진 말로 '동적 배열구조 클래스'라고 한단다.

데이터를 주소 시작점부터 차곡차곡 담아낸다는데, 이런 점 때문에 중간에 데이터를 삽입하는 등 array에서 발생하는 단점이 그대로 존재하긴 한다. 그리고 장점도 그대로 존재하는데 장점은 많으니까 넘어가도록 하자

저장할 데이터의 크기가 정해져있지 않은데 순차접근이나 랜덤접근이 필요할 때는 벡터를 쓰면 좋다고 한다. split 함수에서도 쓰이는데 `#include<vector>` 이걸 위에 헤더로 둬야 쓸 수 있다.

## vector의 문법을 배워보자

아래와 같이 선언하면 타입에 따라서 만들 수 있다. 참고로 위는 벡터 선언이고 아래는 array 선언이다. 'list'는 배열의 이름이다.

```cpp
vector<int> list;
int array[0] = list;
```

디폴트 값으로 벡터를 채우려면 아래처럼 하면 된다. 위에는 int기 때문에 디폴트가 0인 채로 10개가 채워지고 아래는 char이기 때문에 스페이스로 10개가 채워진다.

```cpp
vector<int> list1[10];
vector<char> list2[10];
```

아예 벡터를 초기화시키는 방법도 있는데 `(초기화 이후 개수, 초기화할 값)`을 뒤에 붙여주면 된다. 만약 (5, 2)면 벡터에는 2가 5개 차게 된다. 물론 char이나 string도 가능

```cpp
vector<int> list1(5, 2);
vector<char> list2(5, 'A');
```

벡터에 값을 직접 넣는 것도 가능하다. 중괄호를 쓰는 것이 마치 set을 보는 듯한 기분임 그런데 이것보다 예전 버전을 쓰는 사람은 거의 없겠지만 C++11부터 가능하다 한다. 사용할 때 주의하자.

```cpp
vector<int> list1{1, 2, 3, 4, 5}
vector<char> list2{'a', 'b', 'c'};
```

벡터에 값을 채우는 방법이다. 맨 뒤에 꼬리처럼 달면 배열의 크기가 늘어나는 방식이다. 파이썬에서 list에 `list.append()` 해주는 것처럼 cpp에서는 아래처럼 하면 된다. 이렇게 하면 list라는 벡터에는 총 3개의 값이 담기게 된다.

```cpp
vector<char> list;
list.push_back('a')
list.push_back('b')
list.push_back('c')
```

벡터를 통째로 복사해올 수도 있다. 아래처럼 하면 list1에 있는 5개의 값을 list2로 그대로 복사한다. 연산자가 먹기 때문에 대입 연산자를 사용해도 된다고는 하는데 굳이..? 라는 생각이 든다.

```cpp
vector<int> list1{1, 2, 3, 4, 5};
vector<int> list2(list1);
```

하지만 연산자로 대소비교를 하는 건 많이 쓸 것 같음. `list1 > list2` 같이 비교해서 쓸 수도 있다. `==`이 true이면 사용하면 모든 원소가 같은 것이고, `!=`이 true이면 하나라도 다른 원소가 있는 것이다. `=`는 복사를 하는 것이니 오타를 조심하자.

## cpp에서의 함수

C언어랑 똑같다. 아래는 두 값을 더해서 리턴하는 함수이다.

```cpp
int sum(int a, int b) {
    return a + b;
}
```
