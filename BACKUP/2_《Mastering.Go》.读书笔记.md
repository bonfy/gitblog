# [《Mastering Go》 读书笔记](https://github.com/bonfy/gitblog/issues/2)

书籍链接： https://www.amazon.com/Mastering-production-applications-concurrency-structures-ebook/dp/B07WC24RTQ
Code: https://github.com/PacktPublishing/Mastering-Go

---

调用C程序

cGo.go

```go
package main

//#include <stdio.h>
//void callC() {
//    printf("Calling C code!\n");
//}
import "C"
import "fmt"

func main() {
    fmt.Println("A Go statement!")
    C.callC()
    fmt.Println("Another Go statement!")
}
```

---

复杂点的 调用 C

callClib/callC.h

```c
#ifndef CALLC_H
#define CALLC_H

void cHello();
void printMessage(char* message);

#endif
```

callClib/callC.c
```c
#include <stdio.h>
#include "callC.h"

void cHello() {
    printf("Hello from C!\n");
}

void printMessage(char* message) {
	printf("Go send me %s\n", message);
}

```


callC.go

```go
package main

// #cgo CFLAGS: -I${SRCDIR}/callClib
// #cgo LDFLAGS: ${SRCDIR}/callC.a
// #include <stdlib.h>
// #include <callC.h>
import "C"

import (
	"fmt"
	"unsafe"
)

func main() {
	fmt.Println("Going to call a C function!")
	C.cHello()

	fmt.Println("Going to call another C function!")
	myMessage := C.CString("This is Mihalis!")
	defer C.free(unsafe.Pointer(myMessage))
	C.printMessage(myMessage)

	fmt.Println("All perfectly done!")
}

```


```cmd
$ gcc -c callClib/*.c  
# 当前目录会产生 callC.o

$ ar rs callC.a *.o
# 产生 callC.a
$ file callC.a
callC.a: current ar archive random library

$ rm callC.o

$ go build callC.go
# 产生 可执行 的 callC.exe
$ .\callC.exe
```