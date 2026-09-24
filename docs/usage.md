# 使用文档

面向普通用户的完整说明。安装步骤见仓库 [README](../README.md)。

## 校验下载文件

每个 Release 都附带 `.sha256` 校验文件，发行说明里也写明了哈希值：

```powershell
Get-FileHash .\Firefox_153.0.7z -Algorithm SHA256
```

输出的哈希应当与发行说明里的完全一致。

## 目录结构

解压后是这样，首次运行会自动创建 `Profiles/` 和 `Cache/`：

```text
解压目录/
├── Firefox/                      浏览器本体
│   ├── firefox.exe
│   ├── portable.ini              便携版配置
│   ├── portable64.dll            便携化运行时
│   ├── README                    libportable 说明文档
│   └── LICENSE-libportable.txt   libportable 许可证
├── Profiles/                     用户数据：书签、扩展、登录状态、密码
├── Cache/                        缓存
├── 开始.bat                      创建快捷方式的脚本
└── Firefox.lnk                   运行 开始.bat 后生成的快捷方式
```

**最重要的是 `Profiles/`。** 只要这个目录还在，你的浏览器数据就还在。

## 更新到新版本

更新时只替换浏览器本体，保留 `Profiles/`：

1. 完全关闭 Firefox。
2. 把旧的 `Firefox` 目录改名为 `Firefox_old` 作为备份。
3. 从新版压缩包里解压出 `Firefox` 目录，放到原来的位置。
4. 启动浏览器，确认书签、扩展、登录状态都正常。
5. 确认无误后再删除 `Firefox_old`。

> 不要直接删掉整个解压目录再重新解压，那样 `Profiles/` 里的数据会一起消失。

## 配置说明

配置文件在 `Firefox/portable.ini`，一般不需要改。常用项：

| 配置项 | 默认值 | 说明 |
| --- | --- | --- |
| `Portable` | `1` | 便携模式开关，改成 `0` 就退化成普通安装版行为 |
| `PortableDataPath` | `../Profiles` | 用户数据目录，相对 `Firefox/` 计算 |
| `TmpDataPath` | `../Cache` | 缓存目录 |
| `DisableScan` | `0` | 设为 `1` 可禁止扫描注册表安装第三方扩展和插件 |
| `Update` | `0` | libportable 自带的第三方更新通道，保持关闭 |
| `Bosskey` | 空 | 老板键，可自行配置 |

改完配置需要重启浏览器才会生效。完整参数说明见 `Firefox/README`。

## 便携性是怎么保证的

「构建成功」不等于「真的便携」，所以每个包在发布前都要通过两道检查：

1. **静态检查**：读取 `mozglue.dll` 的 PE 导入表，确认便携化运行时确实被注入。
2. **实际运行检查**：无头启动一次浏览器，确认用户数据真的写进了 `Profiles/`，而不是系统的 `%APPDATA%`。

任何一道没过，构建就会失败、不会发布。安装包本身也会在下载后与 Mozilla 官方公布的 `SHA512SUMS` 逐字节比对，不一致就直接终止构建。

## 常见问题

### 能放在 U 盘里吗？

可以，这正是便携版的用途。建议放在路径简单的目录里，例如 `U:\Firefox`，避免路径过长或含特殊符号。

### 快捷方式创建失败？

先确认 `Firefox\firefox.exe` 存在。存在的话直接双击它也能正常启动，`开始.bat` 只是帮你生成一个方便的快捷方式。

### 杀毒软件报毒？

便携化需要修改浏览器的模块导入表，这类行为容易被安全软件误报。请只从本项目的 Release 页面下载，并用 SHA-256 校验文件核对，再自行判断是否信任。

### 界面是英文的，能换成中文吗？

可以。在浏览器里打开 `设置 → 常规 → 语言`，添加中文语言包即可。也可以自行用 `--lang zh-CN` 构建中文版安装包（见 [development.md](./development.md)）。

### 为什么不要下载 Source code？

`Source code.zip` / `Source code.tar.gz` 是仓库源码，里面没有浏览器。成品只有 `Firefox_<版本号>.7z`。
