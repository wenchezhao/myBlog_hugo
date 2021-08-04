---
title: "go中的切片本质"
date: 2020-12-31T21:29:55+08:00
images:
tags: 
  - go
---

### go中的切片本质

​		是对底层数组的封装，它包含了三个信息：底层数组的指针、切片的长度（len）和切片的容量（cap）。

切片b:=a[3:6]示意图：![62bb45676b868517a346d065f5eb58b](C:/Users/admin/AppData/Local/Temp/WeChat Files/62bb45676b868517a346d065f5eb58b.png)

### 判断切片是否为空

​		要检查切片是否为空，应该使用`len(a) == 0`来判断，而不应该使用`a == nil`来判断。

### 切片数组

​		拷贝前后两个变量共享底层数组，对一个切片的修改会影响另一个切片的内容：

```golang
	a := make([]int, 5) // [0 0 0 0 0]
	a1 := a[:2]    
	a1[0] = 1
	fmt.Println(a)  // [1 0 0 0 0]
	fmt.Println(a1) // [1 0 ]
```

​		使用copy（）函数进行切片的复制，可以迅速地将一个切片的数据复制到另外一个切片空间中：

```golang
	a := []int{1, 2, 3, 4, 5}
	c := make([]int, 5, 5)
	copy(c, a)     //使用copy()函数将切片a中的元素复制到切片c
	fmt.Println(a) //[1 2 3 4 5]
	fmt.Println(c) //[1 2 3 4 5]
	c[0] = 1000
	fmt.Println(a) //[1 2 3 4 5]
	fmt.Println(c) //[1000 2 3 4 5]
```

### 切片的动态扩容

​       每个切片会指向一个底层数组，这个数组的容量够用就添加新增元素。当底层数组不能容纳新增的元素时，切片就会自动按照一定的策略进行“扩容”，此时该切片指向的底层数组就会更换。“扩容”操作往往发生在`append()`函数调用时，所以我们通常都需要用原变量接收append函数的返回值。

```go
func main() {
	var num []int
	for i := 0; i < 10; i++ {
		num = append(numSlice, i)
		fmt.Printf("%v  len:%d  cap:%d  ptr:%p\n", num, len(num), cap(num), num)
	}
}

// [0]  len:1  cap:1  ptr:0xc0000160d0
// [0 1]  len:2  cap:2  ptr:0xc000016100
// [0 1 2]  len:3  cap:4  ptr:0xc00000a3c0
// [0 1 2 3]  len:4  cap:4  ptr:0xc00000a3c0
// [0 1 2 3 4]  len:5  cap:8  ptr:0xc000014300
// [0 1 2 3 4 5]  len:6  cap:8  ptr:0xc000014300
// [0 1 2 3 4 5 6]  len:7  cap:8  ptr:0xc000014300
// [0 1 2 3 4 5 6 7]  len:8  cap:8  ptr:0xc000014300
// [0 1 2 3 4 5 6 7 8]  len:9  cap:16  ptr:0xc000018080
// [0 1 2 3 4 5 6 7 8 9]  len:10  cap:16  ptr:0xc000018080


// append()函数将元素追加到切片的最后并返回该切片
// 动态扩容后的切片地址一般发生了变化
```



