https://github.com/PerimeterX/marshmallow

Marshmallow provides a flexible and performant JSON unmarshalling in Go. It specializes in dealing with unstructured struct - when some fields are known and some aren't, with zero performance overhead nor extra coding needed.

```go
func main() {
	marshmallow.EnableCache() // this is used to boost performance, read more below
	v := struct {
		Foo string `json:"foo"`
		Boo []int  `json:"boo"`
	}{}
	result, err := marshmallow.Unmarshal([]byte(`{"foo":"bar","boo":[1,2,3],"goo":12.6}`), &v)
	fmt.Printf("v=%+v, result=%+v, err=%v", v, result, err)
	// Output: v={Foo:bar Boo:[1 2 3]}, result=map[boo:[1 2 3] foo:bar goo:12.6], err=<nil>
}
```

