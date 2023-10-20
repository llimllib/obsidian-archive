Create a hello world: `dotnet new console -o HelloWorld -f net7.0`

Install the RestSharp package: `dotnet add package RestSharp`

Run a script depending on restsharp using [dotnet-script](https://github.com/dotnet-script/dotnet-script):

```
$ dotnet tool install -g dotnet-script
$ cat test.cs
#r "nuget: RestSharp, 110.2.0"

using RestSharp;

var options = new RestClientOptions("https://httpbingo.org/");
var client = new RestClient(options);
var request = new RestRequest("get");
var response = await client.GetAsync(request);

Console.WriteLine("Response: ", response.Content);
$ dognet-script test.cs
```

