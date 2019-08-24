thist - a go package for calculating online histograms with plotting to the terminal and images
===============================================================================================
[![Documentation](https://godoc.org/github.com/bsipos/thist?status.svg)](http://godoc.org/github.com/bsipos/thist)
[![Go Report Card](https://goreportcard.com/badge/github.com/bsipos/thist)](https://goreportcard.com/report/github.com/bsipos/thist)

Example
-------

```go
package main

import (
        "fmt"
        "github.com/bsipos/thist"
        "math/rand"
        "time"
)

// randStream return a channel filled with endless normal random values
func randStream() chan float64 {
        c := make(chan float64)
        go func() {
                for {
                        c <- rand.NormFloat64()
                }
        }()
        return c
}

func main() {
        // create new histogram
        h := thist.NewHist(nil, "Example histogram", "auto", -1, true)
        c := randStream()

        i := 0
        for {
                // add data point to hsitogram
                h.Update(<-c)
                if i%50 == 0 {
                        // draw histogram
                        fmt.Println(h.Draw())
                        time.Sleep(time.Second)
                }
                i++
        }
}

```

<iframe width="560" height="315" src="https://www.youtube.com/embed/7mrs1QGDyys" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

