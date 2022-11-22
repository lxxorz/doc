有关 http 常用的压缩格式，主要有以下三个
- gzip
- deflate
- brotli
主要简单介绍一下，gzip 和 deflate 两个压缩格式和相关的压缩算法
## 历史
现在所有的无损压缩算法基本上都可以追溯到两个压缩算法 **LZ77**和**LZ78**
LZ77 算法非常简单，它将文本当中一些重复的地方用三元组 $\langle distance, length, character\rangle$ 表示
```js
document.addEventListener("click", f);

document.addEventListener("click", g);
```
看上面这段 JavaScript 代码，LZ77 会怎么处理呢，它将 `document.addEventListener("click", ` 这部分用一个元组替代
```
document.addEventListener("click", f);

<40, 32> g);
```
这里的元组代表什么意思呢？这里的 13 代表向前回退 13 字节，32 代表复制 32 个字节

肉眼可见，整段文本被缩小了，但是有一个很明显的问题是，所谓文件内容在计算机当中都是一些字节，当完成压缩之后，怎么保证文件里面的元组是通过压缩算法生成的而非文件本身的内容如此，LZ77 用了一个显得有点呆瓜的方法，那就是将所有的文字内容通过元组形式表示,所以，假设有以下文本
```
abc
```
那么就会变成
```
<0,0,a><0,0,b><0,0,c><1,1,END>
```
从 `a ==> <0,0,a>` 显然占据的空间更多了，这样直接的方式，肯定在某种情况下会出现不仅不会压缩文件，而且文件本身还会变大的滑稽情况
![[http-compression-lz77.png]]

### LZSS
大概五年之后，LZSS 压缩算法被创建，LZSS 是 LZ77 的变种算法之一，相比于 LZ77 用三元组 $\langle d,l,c\rangle$ 来表示每一个字，LZSS 会用一个 bit 来表示一个字节是字面量还是三元组，
```
00000000 1010101
```


#### Huffman Coding


- 关于 Huffman Tree 的构建过程 [Huffman Coding Visualization (ubc.ca)](https://cmps-people.ok.ubc.ca/ylucet/DS/Huffman.html) 
## gzip
言归正传，所以到底什么是 GZIP 呢，gzip 其实就是 DEFALTE 
![[meme-gzip.png]]
当然，gzip 还在外面包装了一层，增加更多的信息，比如文件名时间戳 循环冗余检验...
也就是这一段 ![[http-compression-gzip-header.png]]

| gzip format       | zlib format|
| ----------- | -------- |
| crc32/crc16 | alter-32 |

而 Deflate 是基于 LZSS 和 Huffman Coding
```mermaid
flowchart TB
	deflate ==> lzss
	deflate ==> h[huffman coding]
```
基本上就是用 LZSS 跑一遍然后用 Huffman  Coding 重新编码

### 网络传输当中如何使用压缩
想要使用压缩，必须客户端支持，浏览器通过指定请求头中的
```
Accept-encoding: gzip br deflate
```
来表明支持**gzip brotli defalte**格式的压缩算法
当请求发送给服务器之后，服务器最终决定使用哪种**压缩算法**，然后通过指定响应头中的
```
Content-Encoding: gzip
```
来告诉浏览器：“hey，我们使用 gzip 吧😘”

当然 Content-Encoding 能够指定的值不只是上面提到的三个，能够使用的选项在 [Hypertext Transfer Protocol (HTTP) Parameters (iana.org)](https://www.iana.org/assignments/http-parameters/http-parameters.xhtml) 能够找到












