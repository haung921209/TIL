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
    ListNode<T>(T value1, ListNode<T> * next1):value(value1),next(next1){};
};
```



```c++
class InvalidIndexException{};

template <typename T>
class LinkedList {
public:
    ListNode<T> *head;
    int size;

    //생성자
    LinkedList<T>(): size(0), head(nullptr){};

    //insert 
    //k번째 원소 앞에 value삽입
    void insert(int k, T value){
        try{
            if(k<0||k>size){
                throw InvalidIndexException();
            }
            else if(k==0){
                head = new ListNode<T>(value, head);
                size++;
            }
            else{
                ListNode<T>* temp=head;
                for(int i=0;i<k-1;i++)
                    temp=temp->next;
                temp->next=new ListNode<T>(value, temp->next);
                size++;
            }
        }
        catch(InvalidIndexException e){
            cerr<<"Invalid index error\n";
        }
    }
    //erase
    //eraseIdx번째에 있는 node 제거.
    void erase (int eraseIdx) {
        try{
            if(eraseIdx < 0 || eraseIdx >= size)throw InvalidIndexException();
            else if(eraseIdx==0){
                ListNode<T> * temp=head->next;
                delete head;
                head=temp;
                size--;
            }
            else{
                ListNode<T> * dest = head, *temp;
                for(int i=0;i<eraseIdx-1;i++)dest=dest->next;
                temp=dest->next->next;
                dest->next=temp;
                size--;
            }
        }
        catch(InvalidIndexException e){
            cerr<<"Invalid index error\n";

        }
    }
    //search
    //있으면 index return, 없으면 -1 return
    int search(T value){
       try{
           ListNode<T> * temp = head;
           for(int i=0;i<size;i++){
               if(temp->value==value)return i;
               temp=temp->next;
           }
           return -1;
        }
        catch(InvalidIndexException e){
            cerr<<"Invalid index error\n";
        }
     }




};
```