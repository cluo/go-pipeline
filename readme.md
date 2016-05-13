Pipeline Supporter
==================

[example](./example/example.go) :

```
package main

import (
    "fmt"
    "github.com/zetamatta/pipeline"
)

func main(){
    fmt.Println("Start")
    pipeline.Run(func(in, out chan interface{}) {
        for i := 0; i < 10; i++ {
            out <- i
        }
    }, func(in, out chan interface{}) {
        for value := range in {
            out <- interface{}(value.(int) + 1)
        }
    }, func(in, out chan interface{}) {
        for value := range in {
            fmt.Printf("%d\n", value.(int))
        }
    })
    fmt.Println("Done.")
}
```
