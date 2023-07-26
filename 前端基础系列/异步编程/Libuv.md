# epoll

## 前置知识
### 阻塞
程序被被分成以下几种状态
- 新生（_new_）：进程产生中。
- 执行（_running_）：正在执行。
- 等待（_waiting_）：等待某事发生，例如等待用户输入完成。亦称“阻塞”（_blocked_）
- 就绪（_ready_）：[排班中](https://zh.wikipedia.org/wiki/%E6%8E%92%E7%A8%8B "调度")，等待CPU。
- 结束（_terminated_）：完成执行




[1] https://zh.wikipedia.org/zh-sg/%E8%A1%8C%E7%A8%8B#%E7%8B%80%E6%85%8B