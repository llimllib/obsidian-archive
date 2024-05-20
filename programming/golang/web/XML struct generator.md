---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/miku/zek

```go
$ curl -s https://raw.githubusercontent.com/miku/zek/master/fixtures/e.xml | zek -e
// Rss was generated 2018-08-30 20:24:14 by tir on sol.
type Rss struct {
    XMLName xml.Name `xml:"rss"`
    Text    string   `xml:",chardata"`
    Rdf     string   `xml:"rdf,attr"`
    Dc      string   `xml:"dc,attr"`
    Geoscan string   `xml:"geoscan,attr"`
    Media   string   `xml:"media,attr"`
    Gml     string   `xml:"gml,attr"`
    Taxo    string   `xml:"taxo,attr"`
    Georss  string   `xml:"georss,attr"`
    Content string   `xml:"content,attr"`
    Geo     string   `xml:"geo,attr"`
...etc
```

