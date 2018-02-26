Wikepedia definition of `class template` - "A class template provides a specification for generating classes based on parameters."

Syntax: ```C++ template <parameter-list> class-declaration.```

Here is described another type of `class` which fits definition from Wikepedia and 
since it is very similar to `class template` but is not exactly the same, it is called `class quasi-template`.

`class quasi-template` is described bellow.

```C++
template <typename T>
auto QuasiX() {
   struct: public std::vector<T> {
     using std::vector<T>::vector;
   }* p = 0;

   return *p;
}

template <typename T>
using X = decltype(QuasiX<T>());

X<int> x = {1, 2, 3};
```

`class quasi-template` can have explicit (full) specialization (bellow), but cannot have partial specialization and cannot have template functions.

```C++
template <>
auto QuasiX<char>() {
   struct {
   }* p = 0;

   return *p;
}
```


`class quasi-template` doesn't seem to be useful, but there is probbaly one case where it could be usefull - when it is used with lambda function:

```C++
void Foo() {
  auto X = [](auto par) {
    uinsg T = decltype(par);

    struct: public vector<T> {
       using std::vector<T>::vector;
    }* p = 0;

    return *p; 
  };

  // Local "class quasi-template" can be instantiated with different types.

  decltype(X(int())) x1 = {1, 2, 3};

  decltype(X(std::string())) x1 = {"1", "2", "3");
}
```

While it is not possible to use local `class template`, it is possible to use local `class quasi-template`, which sometimes could be usefull.


