# golang编程规范

## 1.错误处理

优先处理错误，error在条件判断中优先处理。例如：

```go
for _, item := range list {
	if match, err := item.Execute(ctx); err != nil{
		return err
	} else if !match {
		//no match continue
	} else if err := item.action.Execute(ctx); err != nil {
		return err
	} else if isEnded, err := ctx.Ended(); err != nil {
		return err
	} else if isEnded {
		break
	}
}
```

