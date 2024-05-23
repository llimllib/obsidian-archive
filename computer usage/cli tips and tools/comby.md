---
created: 2024-05-23T12:42:59.784Z
updated: 2024-05-23T12:42:59.784Z
---
https://comby.dev/
https://github.com/comby-tools/comby

> Use lightweight templates to easily search and change code, HTML, or JSON. Comby is designed to work on any language or data format.

> Comby is ideal for touching up pieces of code. Use it to translate code like this Python 2 to 3 fixer on the right to replace deprecated methods. Easily write one-off refactors or a collection of quickfixes customized to your project. Comby makes finding and changing code easier than regex alone allows and avoids pitfalls like escaping parentheses, quotes, or multiline changes.

The example they give:

```bash
comby 'failUnlessEqual(:[a],:[b])' 'assertEqual(:[a],:[b])' example.py
```

```diff
--- example.py
+++ example.py
@@ -1,6 +1,6 @@
     def test(self):
         r = self.parse("if 1 fooze", 'r3')
-        self.failUnlessEqual(
+        self.assertEqual(
             r.tree.toStringTree(),
             '(if 1 fooze)'
             )
```

Written in [[OCaml]], doesn't use [[tree-sitter]] which surprised me a bit.

see also [[fastmod]], [[ast-grep]]