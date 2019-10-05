LinkedList(링크드리스트)
====================

--------
```c++
template <typename T>
class ListNode{
public:
    T value;
    ListNode<T> * next;

    //생성자
    ListNode<T>():next(nullptr){};
};
```



```c++
template <typename T>
class LinkedList {
public:
    ListNode<T> *head;
    int size;

    //생성자
    LinkedList<T>(): size(0), head(nullptr){};

    




};
```