# 现代 web 布局
## Trick one
由于 `align-items` 属性的初始值为 `stretch` ，每个 Flex 项目在侧轴方向被拉伸，Flex 项目高度变高填充了 Flex 容器侧轴空间（即 Flex 容器的 `height` 或 `block-size`），并且每行的 Flex 项目高度是相等的。

## Trick two
If the block-size or height is specified explicitly, even if the align-items properties set to `scratch`, the original value still be maintained.

## Limitation

The flex layout doesn't have justify-self property in the main axis because the main axis is regarded as a group. 

Therefore, if you want to justify single items along main axis, you should utilize the grid layout.



## playground

https://codepen.io/lxxorz/pen/NWLrPVL