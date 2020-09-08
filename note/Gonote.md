# 我的GOLANG学习笔记

本人自学习计算机以来，对C/C++情有独钟，在准备毕业设计的时候接触到了Go这门语言，在完成毕设之后对其婶婶不能忘记，于是打算好好学习一下这门语言，这篇笔记是我根据自己对于其他论坛了书籍的大佬的知识的总结而总结的，希望共同努力，一起成长。
- 参考书籍《Go学习笔记》
- 官网文档

## &源文件
这一章主要说明Go的一些需要特别注意的东西和知识点。Go兼容C的很多语法和注释，但是Go的语句不需要强制使用分号进行结束语句，但是要注意好空格和回车的使用。同时，Go和C一样是有入口main函数的，main函数没有参数。

## &变量
在C语言中我们定义一个变量的方法很有限，在Go中我们可以使用 `:=` 来对变量进行模糊定义赋值。格式
`name  type := value`
当然你也可以使用var来对变量进行定义和赋值。

## &表达式
判断语句`if`
```
func main () {
	x := 100
	if x > 0 {
		fmt.Print("x")
	} else if x < 0{
		fmt.Println("-x")
	} else {
		fmt.Print("0")
	}
}
```
选择语句`switch`
```
func main () {
	x := 100
	switch {
	case x > 0:
		fmt.Println("x")
	case x < 0:
		fmt.Println("-x")
	default:
		println("0")
	}
}
```
循环语句`for`
```
func main () {
	for i := 0; i < 5; i++ {
		fmt.Println(i)
	}
}
```
迭代循环`for...range`
```
func main () {
	x := []int{100,101,102}
	for i, n := range x{
		fmt.Println(i, ":", n)
	}
}

```

## &函数
在Go中函数有多种使用方法
```
func div(a, b int) (int, error) {
	if b == 0 {
		return 0, errors.New("division by zero!")
	}
	
	return a / b, nil
}
```
同时函数也是第一类型可以作为参数或者返回值
```
func test (x int) func() {
	return func() {
		println(x)
	}
}
```
我们也可以使用`defer`定义延迟调用，无论函数是否有错，它都会确保结束前被调用
```
func test (a, b int){
	defer println("dispose...")
	println(a / b)
}
```

## &数据
切片(slice)类似动态数组的功能
```
func test () {
	x := make([]int, 0, 5) //创建容量为 5 的切片
	for i := 0; i < 8; i++ {
		x = append(x, i) //追加数据，当超出容量时，自动分配更大的储存空间
	}
	fmt.Println(x)
}
```
字典(map)
```
func test() {
	m := make(map[string]int) //创建字典类型对象
	m["a"] = 1                //添加或设置
	x, ok := m["b"]           //使用ok-idiom获取值，可知道key/value是否存在
	fmt.Println(x, ok)
	delete(m, "a") 	  //删除
}
```
结构体(struct)可匿名嵌入其他数据类型
```
type manager struct {
	name string
	time int
}

type author struct {
	manager
	title string
}

```

## &方法
和Java等语言概念一样
```
func test(x int) int {
	return 0
}

```
