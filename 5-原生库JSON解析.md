## Go语言JSON解析相关说明
Go语言提供了`encoding/json`包来支持JSON的解析和生成。该包中包含了`Marshal`和`Unmarshal`两个函数分别用于将`struct`结构体转换为JSON格式的数据和将JSON格式的数据转换为`struct`结构体
## 解析JSON
```go
// ----------------示例（单层JSON对象结构解析方法）----------------
package main

import (
	"encoding/json"
	"fmt"
)

type Person struct {
	Name string `json:"name"` //指定JSON的key别名，可选
	Age  int    `json:"age"`
}

func main() {
	var p Person
	jsonString := `{ "name": "LingCai",
    "age": 18}`
    //调用json包里的Unmarshal方法实现解析JSON字符串
	err := json.Unmarshal([]byte(jsonString), &p)
	if err == nil {
		fmt.Println(p.Name)
		fmt.Println(p.Age)
	} else {
		fmt.Println(err)
	}
}
// ----------------示例（嵌套JSON对象结构解析方法）----------------
package main

import (
	"encoding/json"
	"fmt"
)

type Person struct {
	Name    string `json:"name"`
	Age     int    `json:"age"`
	Address struct {
		City string `json:"city"`
	}
}

func main() {
	var p Person
	jsonString := `{ "name": "LingCai",
    "age": 18, "address": { "city": "Nanjing" }}`
	err := json.Unmarshal([]byte(jsonString), &p)
	if err == nil {
		fmt.Println(p.Name)
		fmt.Println(p.Age)
		fmt.Println(p.Address.City)
	} else {
		fmt.Println(err)
	}
}
// ----------------示例（数组JSON对象结构解析方法）----------------
package main

import (
	"encoding/json"
	"fmt"
)

func main() {
	var m map[string]any

	jsonString := `{ "name": "LingCai",
    "age": 18, "addresses": ["Nanjing", "Beijing"]}`
	err := json.Unmarshal([]byte(jsonString), &m)
	if err == nil {
		fmt.Println(m["name"])
		fmt.Println(m["age"])
		fmt.Println(m["addresses"])
	} else {
		fmt.Println(err)
	}
}

```