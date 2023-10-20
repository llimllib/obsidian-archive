To profile a section of ruby code usefully:  

1.  create a directory named `prof`
2.  surround the code you want to profile with:

```ruby
require 'ruby-prof'
result = RubyProf.profile do
  <your code>
end
printer = RubyProf::GraphHtmlPrinter.new(result)
File.open("prof/graph.html", 'w') { |file| printer.print(file, min_percent: 1) }
printer = RubyProf::CallStackPrinter.new(result)
File.open("prof/callstack.html", 'w') { |file| printer.print(file, min_percent: 1) }
```

then look at `prof/callstack.html` and `prof/graph.html`. I found the callstack graph very useful.

https://collectiveidea.com/blog/archives/2012/11/12/tests-oddly-slow-might-be-bcrypt

suggests this route:

```
gem install perftools.rb
CPUPROFILE=profiled RUBYOPT="-r`gem which perftools | tail -1`" rspec spec/
pprof.rb --pdf profiled > profiled.pdf
```

which creates a graphviz-looking call graph