


参考
[Understanding Streams in Node.js - NodeSource](https://nodesource.com/blog/understanding-streams-in-nodejs/)

考虑这样一个场景，有一个很大的文件 1GB，我们需要统计整个文件中字符 n 的个数，但是计算机内存只有 500MB, 那么显然是不能够一次性，全部将文件内容读取出来，对于这个需求而言，也没有必要一次性将文件全部读进内存
通常我们的做法是，一部分一部分的读取，我们将整个文件“分割”成 N 个部分，每次只处理一个部分


![[Pasted image 20221109122807.png]]