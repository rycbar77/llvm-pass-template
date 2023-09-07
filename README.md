# llvm-pass

Clang/LLVM 15.

Build:

    $ mkdir build
    $ cd build
    $ cmake ..
    $ make

Run:

    $ clang++ -fno-discard-value-names -Xclang -disable-O0-optnone  -S -emit-llvm ./main.cpp -o main.ll
    $ clang++ -fno-discard-value-names -Xclang -disable-O0-optnone -fpass-plugin=build/mypass/libMyPass.so main.cpp -o main 
    $ opt -disable-output \
    -load-pass-plugin=build/mypass/libMyPass.so \
    -passes="my-pass" -S main.ll
    $ make && make test