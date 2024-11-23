## C

* Volatile keyword
    The volatile keyword tell the compiler that the variable next to it may change at any time of the program execution and should not be optimized.
    Useful when:
    - INTERFACE WITH HARDWARE: When you interface with hardware that changes the value itself
    - MULTITHREADING: when there's another thread running that also uses the variable
    - SINGAL HANDLER: when there's a signal handler that might change the value of the variable.
* Static keyword
    - static variable inside a function; The variable will keeps its value between the function calls
    - static global variable limits the visibility of the variable or function to the current translation unit. Each of the translation units will have a static global variable of its own.
    - static function is only visible in the same translation unit
* Extern keyword 
    - global variable that can be accessed from multiple translation units, the declaration should be stored in a header file.

* Translation Unit
    - compilation unit and translation unit is the same thing, different wording
    - translation unit is the output of the preprocessor, which looks for all the preprocess directives (#include, #ifdef, macros etc) and expands them.
    Preprocessor only does text manipulation, replaces text with its expansion
    - A translation unit is a single source file and everything that's pulled into that one file using #include statements, headers are pulled recursively. 
    #include directives are literally included, sections of code within #ifndef may be included, and macros have been expanded
    - *.o* or *.obj* files

* Library
    - is a compiled version of the source code and NOT the source code itself. The compiler used to compile the library must be compatible with one that compiles your own source code files.
    - STATIC: the library object code is included in the executable
    - DYNAMIC: Dynamic Link Library or DLL in Windows and Shared Library or SO in Linux: The code to find the library in a shared resource is included

* MMU - memory management unit
    support for address translation, used for virtual memory

## C++

* auto, when does it copy data and when does it get a reference? How does it work internally?
* where are global variables allocated?
    Global variables have static storage duration. They are stored in an area that is separate from both "heap" and "stack".
    Global constant objects are usually stored in "code" (also known as "text") segment, while non-constant global objects are stored in the "data" segment.

    [stack answer](https://stackoverflow.com/a/44360074/11287083)
    Many C toolchains have two segments for global variables: One (traditionally called "data" in Unix land) is for global variables with compile-time-constant initializers, 
    and the other (traditionally called "BSS") for globals that get initialized at run-time. The executable file contains the actual initial values for the variables in the "data" segment, 
    but for the BSS it only has to say how big to make it. –


* what is storage duration in c/c++?
    The storage duration is the property of an object that defines the minimum potential lifetime of the storage containing the object. [cppreference article](https://en.cppreference.com/w/cpp/language/storage_duration).
    There are multiple types of storage duration: 
        - static storage duration 
        - thread storage duration (since C++11)
        - automatic storage duration
        - dynamic storage duration 

    [one great answer on stack](https://stackoverflow.com/a/76970208/11287083)

* what are the data, rodata and bss sections?
    - [data](https://en.wikipedia.org/wiki/Data_segment)
    - [bss](https://en.wikipedia.org/wiki/.bss)

* rvalue, lvalue, prvalue, xvalue, glvalue
    - one answer from [reddit](https://www.reddit.com/r/cpp/comments/6wpnkp/comment/dmac0x1/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)
    - first step article, [rvalue vs lvalue](https://eli.thegreenplace.net/2011/12/15/understanding-lvalues-and-rvalues-in-c-and-c)


auto nie dedukuje referencji, auto &x, bez referencji
decltype zwraca typ z wyrażenia, dedukuje dokładnie to co mu się przekaże, decltype(auto)?
reference collapsing rules
constexpr
czy globalne zmienne są na stercie albo na stosie?
problem fragmentacji pamięci
what is storage duration in c/c++?
leak i address sanitizer śledzą wycieki pamięci, możesz manualnie śledzić stertę
raii???
unique lock, scope lock, fstream
copy construktor vs move construktor
std::move jest castem bezwarunkowym, std::forward 
każda wartość w C++ ma typ i kategorię
koszt polimorfizu, na przykład tablica vtable
const & vs just &
move only types C++11, na przykład unique pointer

* atomic operation
    Atomic operations in C programming are a set of instructions that are executed as a single, indivisible step. 
    This means other threads or processes cannot interrupt an atomic operation once started.

* cache operations
    - invalidate: mark cache as invalid, so that future read are from the main memory
    - flush: write back form cache to the main memory
