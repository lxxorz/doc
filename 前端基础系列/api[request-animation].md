## request animation
在过去，通过 JavaScript  制作网页动画通常是使用 `setinterval` 来实现的，由于 `setinterval` 是运行在 JavaScript 主线程，在计算量比较大的场景下动画就会阻塞主线程。
![[chrome-thread.png|700]] 



## reference
[1] https://developer.chrome.com/blog/inside-browser-part3/