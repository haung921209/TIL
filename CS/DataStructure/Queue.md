Queue(큐)
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
    ListNode<T>(T value1, ListNode<T> * next1):value(value1),next(next1){};
};
```

```c++
class InvalidIndexException{};
```





```c++
template <typename T>
class Queue{
public:
    ListNode<T>* head;
    ListNode<T>* tail;
    int size;

    //생성자
    Queue<T>(): size(0), head(nullptr), tail(nullptr){};

    //insert
    void insert(T value){
        ListNode<T> temp = new ListNode(T,nullptr);
        tail=temp->next;
        size++;
    }
    //pop
    //갯수가 없는 경우 invalid index 예외 발생
    //
    void pop(){
        try{
            if(size<=0)throw InvalidIndexException();
            head=head->next;
            size--;
        }
        catch(InvalidIndexException e){
            cerr<<"Invalid index exception is occured\n";

        }
    }
    //front value return
    //값이 없을시에는 -1 리턴(값 범위에 따라 변경 요)
    T front(){
        if(size>0)
            return head->value;
        else
            return -1;
    }


}


```