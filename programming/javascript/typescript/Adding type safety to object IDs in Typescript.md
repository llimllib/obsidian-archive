---
updated: '2024-01-31T14:38:04Z'
created: '2024-01-31T14:38:04Z'
---
https://www.kravchyk.com/adding-type-safety-to-object-ids-typescript/

The article introduces [template literal types](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-4-1.html) in typescript:

```typescript
type NodeId = `node_${string}`
```

Which is, as you might guess, a type representing of strings beginning with `node_`