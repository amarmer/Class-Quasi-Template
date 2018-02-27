
# Class quasi-template

Bellow is definition of `class template` from Wikipedia:<br/>
```A class template provides a specification for generating classes based on parameters.```

Here is described another type of `class` which fits this definition and since it is similar to `class template` 
but is not exactly the same (and doesn't have it's syntax ```template <parameter-list> class-declaration```), it is called `class quasi-template`.

`class quasi-template` is described bellow.

```C++
template <typename T>
auto QuasiList() {
   // This is example of 'class quasi-template'.
   struct: public std::vector<T> {
     using std::vector<T>::vector;
   }* p = 0;

   return *p;
}

template <typename T>
using List = decltype(QuasiList<T>());

// 'class quasi-template' can be used exactly as 'class template'.
List<int> list1 = {1, 2, 3};
List<str::string> list2 = {"1", "2", "3}; 
```

`class quasi-template` cannot have partial specialization and cannot have template functions,<br/>
but can have explicit (full) specialization:

```C++
template <>
auto QuasiList<char>() {
   struct {
   }* p = 0;

   return *p;
}
```

`class quasi-template` doesn't seem to be useful, except probably one case - when it is used with lambda function:

```C++
void Foo() {
  auto List = [](auto par) {
    using T = decltype(par);

    struct: public vector<T> {
       using std::vector<T>::vector;
    }* p = 0;

    return *p; 
  };

  // Local "class quasi-template" can be instantiated with different types.

  decltype(List(int())) list1 = {1, 2, 3};

  decltype(List(std::string())) list2 = {"1", "2", "3");
}
```

While it is not possible to use local `class template`, it is possible to use local `class quasi-template`,<br/>
which sometimes could be usefull.


