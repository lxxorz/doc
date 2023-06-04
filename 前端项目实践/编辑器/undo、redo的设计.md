# Undo Redo 的设计
撤销和重做是一个编辑器当中的通用功能。

## op-based
+ `add(obj)`
+ `delete(obj)`
+ `edit(obj)`

```mermaid
flowchart LR
add1 --> add2 --> delete2 --> delete1
```

if user undo N times , he must be can back to newest state.

| sid     | property     |
| ------- | ------------ |
| 4234123 | {property 1} |

== Command generating
the new and old both are object that contain SID.

| op     | result  |undo|
| ------ | ------- | ----|
| add    | - new     | `delete(new)` |
| delete | old -     | add(old) ` |
| edit   | old-new | `replace(old)` |

### Command Stack

```mermaid
graph LR
subgraph Redo Stack
  D(add-1) --> E(replace-2) --> F(delete-1)
end

subgraph Undo Stack
  A(add-1-old) --> B(replace-2-old) --> C(delete-1-new)
end

C==>D;

```

`2k => w ==> 20MB`