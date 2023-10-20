I made an SVG that displays a chess board, but it uses a path - I think I will want one that uses squares instead, so that I can drag + drop things onto them.

Also worth thinking about how to easily style the board

```
<svg xmlns="http://www.w3.org/2000/svg" width="500" height="500" viewBox="0 0 8 8">
<rect width="8" height="8"/>
<path d="M0,0v8h1V0zM2,0v8h1V0zM4,0v8h1V0zM6,0v8h1V0zM8,0v8h1V0zM0,0h8v1H0zM0,2h8v1H0zM0,4h8v1H0zM0,6h8v1H0zM0,8h8v1H0z"
    fill="#fff"
    fill-rule="evenodd"/>
</svg>
```

The docs for [path commands](https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/d#path_commands) and [fill rule](https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/fill-rule) were helpful in understanding this