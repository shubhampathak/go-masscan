# go-masscan

go-masscan is a golang library to run masscan scans, parse scan results.


## Installation


```sh
go get github.com/shubhampathak/go-masscan
```
to install the package

```go
import "github.com/shubhampathak/go-masscan"
```

## Example

```go
package port

import (
	"fmt"
	"time"

	"github.com/shubhampathak/go-masscan"
)

var t = time.Now()

//Port Scan arguments for all functions in /vendor/github.com/dean2021/go-masscan/masscan.go
func Port(c *gin.Context) {

	m := masscan.New()

	m.SetInput("path/to/ip_list.txt")
	m.SetPorts("1-65535")
	m.SetRate("1000")
	m.SetOutput("results_" + t.Format(time.RFC3339) + ".xml") //Export results.xml with timestamp

	err := m.Run()
	if err != nil {
		fmt.Println("Scan Failed:", err)
		return
	}

	results, err := m.Parse()
	if err != nil {
		fmt.Println("Parsed Scan Result:", err)
	}

	for _, result := range results {
		fmt.Println(result)
	}
}

```
