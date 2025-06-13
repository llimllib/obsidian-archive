https://git.peppe.rs/languages/tbsp/about/

> tbsp is an awk-like language that operates on tree-sitter syntax trees. to motivate the need for such a program, we could begin by writing a markdown-to-html converter using tbsp and tree-sitter-md [0]...

```
BEGIN {
	int depth = 0;

	print("<html>\n");
	print("<body>\n");
}

# read the README for more

END {
	print("</body>\n");
	print("</html>\n");
}
```

