<!-- YAML
added: v12.12.0
-->

* 返回: {fs.Dirent} 的 {AsyncIterator}

通过 readdir(3) 异步地遍历目录，直到读取了所有的目录项。

异步迭代器返回的目录项始终为 [`fs.Dirent`]。 
`dir.read()` 中为 `null` 的情况会在内部处理。

有关示例，请参阅 [`fs.Dir`]。

该迭代器返回的目录项不遵循操作系统的底层目录机制所提供的特定顺序。
