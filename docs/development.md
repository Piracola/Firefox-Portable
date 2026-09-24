# 开发文档

普通用户请看 [usage.md](./usage.md)。本节面向维护者。

## 自动构建

本仓库不保存浏览器文件，成品由 GitHub Actions 每天自动构建。仓库里只有三样东西：

| 文件 | 作用 |
| --- | --- |
| `portable/portable.ini` | Firefox 专属的便携化配置 |
| `开始.bat` | 创建快捷方式的启动脚本 |
| `.github/workflows/` | 调用通用构建器的工作流 |

下载、校验、解包、注入、打包的逻辑全部在通用构建器 [Gecko-Portable](https://github.com/Piracola/Gecko-Portable) 里，浏览器仓库共用同一套流程。

## 本地构建

维护者想在本地复现构建：

```powershell
# 准备：Python 3.10+、7-Zip
git clone https://github.com/Piracola/Gecko-Portable.git builder
pip install -r builder/requirements.txt

# 构建最新版
python builder/build.py --browser firefox --auto-version `
  --portable portable --launcher 开始.bat

# 想要中文版 Firefox
python builder/build.py --browser firefox --auto-version --lang zh-CN `
  --portable portable --launcher 开始.bat
```

成品是当前目录下的 `Firefox_<版本号>.7z`。

更多参数见 [Gecko-Portable 的 usage 文档](https://github.com/Piracola/Gecko-Portable/blob/main/docs/usage.md)。
