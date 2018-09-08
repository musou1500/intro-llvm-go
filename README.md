## introduction to llvm in go

emits llvm code that returns `35 + 16`

```bash
$ ./intro-llvm-go
; ModuleID = 'my_module'
source_filename = "my_module"

define i32 @main() {
entry:
  %a = alloca i32
  store i32 35, i32* %a
  %b = alloca i32
  store i32 16, i32* %b
  %b_val = load i32, i32* %b
  %a_val = load i32, i32* %a
  %ab_val = add i32 %a_val, %b_val
  ret i32 %ab_val
}
51
```

## build

```
$ release=RELEASE_600
$ svn co https://llvm.org/svn/llvm-project/llvm/tags/$release/final $GOPATH/src/llvm.org/llvm
$ cd $GOPATH/src/github.com/musou1500/intro-llvm-go
$ export CGO_CPPFLAGS="`llvm-config-6.0 --cppflags`"
$ export CGO_CXXFLAGS=-std=c++11
$ export CGO_LDFLAGS="`llvm-config-6.0 --ldflags --libs --system-libs all`"
$ go build -tags byollvm
```

## reference
[Go言語で利用するLLVM入門](https://postd.cc/an-introduction-to-llvm-in-go/)
