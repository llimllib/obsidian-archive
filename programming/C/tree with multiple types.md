---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
David Beazely [said on twitter](https://twitter.com/dabeaz/status/1579084732125827073) that it's not easy to make something like python's `[ '+', ['*', 'a', 'b'], ['*', 'c', ['+', 'd', 'e']], 'f']` in C++; I didn't think it was that hard, and I only know C, so I came up with some code.

I'm a bit proud of it because I'm not a C coder - obviously it's 75 lines of code to replace 1, so it's not that great on that metric - and mostly I'm saving it here because it represents a bit of understanding I gained today and am likely to lose in a month.

```c
#include <stdio.h>

typedef struct tree tree;

typedef enum valtype {
    INT,
    STR,
    TREE
} valtype;

typedef union val {
    char* string;
    int integer;
    tree* child;
} val;

typedef struct datum {
    valtype type;
    val value;
} datum;

struct tree {
  struct datum* children[256];
};

void print_tree(tree *t) {
    printf("[");
    for (int i=0; i < 256; i++) {
        if (t->children[i] == NULL) break;
        switch(t->children[i]->type) {
            case INT:
                printf(" %d ", t->children[i]->value.integer);
                break;
            case STR:
                printf(" \"%s\" ", t->children[i]->value.string);
                break;
            case TREE:
                print_tree(t->children[i]->value.child);
                break;
        }
    }
    printf("]");
}

int main() {
    tree root = { .children = {
        &(datum) { .type = STR, .value = { .string = "+"} },
        &(datum) { .type = TREE, .value = { .child = &(tree) {
            .children = {
                &(datum) { .type = STR, .value = { .string = "*"} },
                &(datum) { .type = INT, .value = { .integer = 7} },
                &(datum) { .type = INT, .value = { .integer = 9} },
            }}
        }},
        &(datum) { .type = TREE, .value = { .child = &(tree) {
            .children = {
                &(datum) { .type = STR, .value = { .string = "*"} },
                &(datum) { .type = STR, .value = { .string = "c"} },
                &(datum) { .type = TREE, .value = { .child = &(tree) {
                    .children = {
                        &(datum) { .type = STR, .value = { .string = "+"} },
                        &(datum) { .type = INT, .value = { .integer = 12} },
                        &(datum) { .type = INT, .value = { .integer = 13} },
                    }}}
                },
                &(datum) { .type = STR, .value = { .string = "d"} },
            }}
        }}
    }};

    print_tree(&root);
    printf("\n");

    return 0;
}
```

compile and run:

```
$ gcc dabeaz.c -o ./dabeaz; ./dabeaz
[ "+" [ "*"  7  9 ][ "*"  "c" [ "+"  12  13 ] "d" ]]
```

things I would do in a real world:
- function to allocate nodes on the stack
- use a stretchy buffer instead of a 256-element array
- figure out if I'm relying on UB by checking for NULL or I need an explicit terminator