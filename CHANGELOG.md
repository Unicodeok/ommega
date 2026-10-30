# A 端模块更新日志

[English](CHANGELOG.en.md)

## 1.7.11

- 本地兜底的 SOTER 密钥改成真机的形状：一把 ATTK 下面每个 uid 各一把 ASK（用到才生成、落盘复用），ASK 再各自挂 AuthKey。以前所有应用共用一把 ASK。
- 上层只需要提供 ATTK 一把（WebUI 或发版内置），ASK 由程序自己生成，对用户透明；removeAllUidKey 会连该 uid 的 ASK 一起删掉。
- 修掉锁屏/解锁周期后整条 ommega 路由变成 SYSTEM_ERROR 4 的问题：零身份的 auth token 不再被当成错误拒绝，镜像恢复也不会因为一条业务拒绝就把所有路由 fail-close（PR #10）。
- 本地兜底 SOTER 的每 uid ASK、AuthKey 都收进 soter_asks.json 一个文件，不再按 uid 散成一堆 pem；AuthKey 也落盘了，payload 重新注入后不用重建。
