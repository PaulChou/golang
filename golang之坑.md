# golang之坑

## 1.range之坑

```go
func Test(){
  num := []int{1,2,3}
	for index,value := range num{
		fmt.Printf("value:%d,value point:%p,num[index] point:%p\r",value,&value,&num[index])
	}
	data := map[string]string{
		"key1":"value1",
		"key2":"value2",
		"key3":"value3",
	}
	for key,value := range data{
		fmt.Printf("%s:%s key point:%s,value point:%s",key,value,&key,&value)
	}
}
```

 测试运行结果：

```
 value:1,value point:0xc420014258,num[index] point:0xc420016100
 value:2,value point:0xc420014258,num[index] point:0xc420016108
 value:3,value point:0xc420014258,num[index] point:0xc420016110
 key1:value1 key point:0xc42004e630,value point:0xc42004e640
 key2:value2 key point:0xc42004e630,value point:0xc42004e640
 key3:value3 key point:0xc42004e630,value point:0xc42004e640
```

从结果可以看到slice的range的value的地址是同一个，map range的key、value的地址也是同一个。如果根据range的value地址来进行传递，所有获取的值将都是一样的。这里的原因是因为range的value是迭代过程产生的新变量，变量的地址是一样的。

## 2.指针类型



