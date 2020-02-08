String
=========


```cpp
string a.b;
a="HELLO WORLD"
b=a.substr(0,4)//[0,0+4)까지의 길이

```

substring은, string type S에 대해 S.substr(pos, count)로 호출시에 [pos, pos+count-1] 범위의 string을 return하는 함수입니다.




```cpp
    string temp = string(count, charT)
```
temp라는 string type 변수를 charT로 count만큼 채운 string type 변수로 초기화하는 생성자 사용 방법.
