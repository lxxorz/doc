问题起源于 2019 年五月的某个 issue 讨论
[Chunk hashes should be based on the output · Issue #2839 · rollup/rollup (github.com)](https://github.com/rollup/rollup/issues/2839)

在使用了 output specify plugins 之后 rollup 的输出的 chunk 文件名当中的 hash 没有发生改变

rollup 维护者在 3.0 修复了此问题
[[v3.0] New hashing algorithm that "fixes (nearly) everything" by lukastaegert · Pull Request #4543 · rollup/rollup (github. com)]( https://github.com/rollup/rollup/pull/4543 )
