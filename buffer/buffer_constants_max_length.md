<!-- YAML
added: v8.2.0
-->

* {integer}  单个 `Buffer` 实例允许的最大内存。

在 32 位的架构上，该值当前是 `(2^30)-1` (~1GB)。
在 64 位的架构上，该值当前是 `(2^31)-1` (~2GB)。

也可使用 [`buffer.kMaxLength`]。

