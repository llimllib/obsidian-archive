Golang really wants the json you parse to be of a known shape; but sometimes you get json of the form:

```json
{ type: "email", data: { "subject": ..., "body": ...} }
```

Where you need to know the `type` before you know how to parse the `data`.

https://eagain.net/articles/go-dynamic-json/ is a good overview of how to handle that situation in go. The meat of it is to parse the top level once, then parse the rest based on the result:

```go
type Envelope struct {
	Type string
	Data interface{}
}

type Email struct {
	Subject string
	Body    string
}

func main() {
	var msg json.RawMessage
	env := Envelope{
	    Type: &msg,
	}
	if err := json.Unmarshal([]byte(input), &env); err != nil {
	    log.Fatal(err)
	}
	switch env.Type {
	case "email":
	    var e Email
	    if err := json.Unmarshal(msg, &e); err != nil {
	        log.Fatal(err)
	    }
	    fmt.Println(e.Body)
	default:
	    log.Fatalf("unknown message type: %q", env.Type)
	}
}

```

