## 单机版爬虫准备-正则表达式

爬取网络信息，email的正则表达式。格式为： **xxx@xxx.xxx**


    1. 从"My email is ccmouse@gmail.com"提取出email地址。


```go
package main

import (
    "regexp"
    "log"
    "fmt"
)

const Text="My email is ccmouse@gmail.com"

func main(){
    re,err:=regexp.Compile("ccmouse@gmail.com")   //知道email地址直接匹配，非常不便
    if err!=nil{
        log.Fatal(err)
        return
    }
    match:=re.FindString(Text)
    fmt.Println(match)
}
```

    2. 使用进阶版的正则表达式


```go
package main

import (
	"regexp"
	"fmt"
)

const text = `My email is ccmouse@gmail.com
email1 is abd@qq.com
email2 is cas@gmail.com.cn
`

func main() {
	//()里面为用正则表达式提取出信息
	re:=regexp.MustCompile(`([a-z0-9A-Z]+)@([a-z0-9A-Z]+)(\.[a-z0-9A-Z.]+)`)
	//找到字符串中所有的email地址
	match:=re.FindAllStringSubmatch(text,-1)
	for _, m := range match {
		fmt.Println(m)
	}
}
```

***执行结果，如下图：***

 ![image](https://raw.githubusercontent.com/wiki/AlexBruceLu/Linux/regexp1.png) 
