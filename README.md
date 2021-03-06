## Proof-of-Work Hashcash 测试

测试页面：[http://121.43.101.95/login.php](http://121.43.101.95/login.php)

每次访问登录页时，会生成一个随机字符串 `pow_ques`。

提交时，需提供一个 `pow_answ` 参数，符合：

```
left(md5(pow_ques + pow_answ), 6) == '000000'
```

因为散列的结果不可预测，只能通过暴力求解。

为了提高性能，本例使用 asm.js，可达到 Native 的 70% 左右。

对于不支持 HTML5 的浏览器，使用 Flash 计算，效率比 asm.js 略低。

为了不阻塞用户体验，使用 WebWorker 多线程计算。对于 Flash 插件，版本必须高于 11.4。


## 缺陷

Hashcash 有很大的弱点，每次计算不依赖之前结果，因此大量并发计算可轻松解题，尤其适用于 GPU。

## 改进

更好的方案是 slowhash，散列重复千万次，类似 bcrypt。即可将并行计算变成串行，降低硬件上的差异。

同时尝试 UGC 模式，利用每个用户的空闲 CPU，参与问题和答案的贡献。以及增加信任机制，让大多数正常用户的结果对抗少量恶意用户。

下回更新。
