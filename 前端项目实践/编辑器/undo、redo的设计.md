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
graph BT
subgraph Cancel Stack
  D(add-1) --> E(edit-2) --> F(delete-1)
end

subgraph Command Stack
  A(add-1) --> B(edit-2) --> C(delete-1)
end

```

`2k => w ==> 20MB`