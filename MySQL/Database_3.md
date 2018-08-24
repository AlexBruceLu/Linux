## 安装Go连接MySQL的驱动

### 环境Ubuntu 18.04.1 + go version go1.10.3 linux/amd64

**1.下载并导入数据库驱动包官方不提供实现，先下载第三方的实现，这里选择了Go-MySQL-Driver这个实现。
地址是：https://github.com/go-sql-driver/mysql/。**

**2.Alt + Ctrl + t命令行输出：go get github.com/go-sql-driver/mysql**

**3.GOPATH下会出现以下文件夹：/src/github.com/go-sql-driver/mysql，此时Go-MySQL驱动安装成功**


### 用一个简单的代码测试下自己的Go-MySQL驱动

```go
package main

import (
	"database/sql"
	"fmt"
	"log"
	_ "github.com/go-sql-driver/mysql"
)

func main() {

	db,err :=sql.Open("mysql","MySQL用户名:MySQL密码@tcp(127.0.0.1:3306)/huoying");
	if err!=nil {
		fmt.Println("sql.Open err:",err)
		return
	}
	defer db.Close()
	err = db.Ping()
	if err != nil{
		fmt.Println("ping fail")
		log.Fatal(err)
	}else{
		fmt.Println("ping success")
	}
	var heroId int
	var heroName string

	err =db.QueryRow("SELECT heroId,heroName FROM hero WHERE heroName = '漩涡鸣人';").Scan(&heroId,&heroName)

	if err != nil{
		log.Fatal(err)
	}

	fmt.Println(heroId,heroName)

}
```


***执行结果！！！***


 ![image](https://raw.githubusercontent.com/wiki/AlexBruceLu/Linux/MySQL_1.png)

***源数据表信息***


 ![image](https://raw.githubusercontent.com/wiki/AlexBruceLu/Linux/MySQL_2.png)
