# 我的第一个仓库

这是我在 DeepSeek Harness 里，用**便携版 Git** 创建的第一个 Git 仓库。

## 我学到了什么

| 命令 | 作用 |
|---|---|
| `git init` | 把一个普通文件夹变成 Git 仓库（生成隐藏的 `.git` 目录） |
| `git status` | 看哪些文件改了、还没提交 |
| `git add <文件>` | 把改动放进"待提交"清单（暂存区） |
| `git commit -m "说明"` | 把清单存成一个历史快照 |
| `git log --oneline` | 回看所有快照 |

## 时间线

- 2026-10-02 创建仓库，完成第一次提交
- 2026-10-02 完成第二次提交，走通完整循环：改文件 → `add` → `commit` → `push`
- 2026-10-02 学会用 Personal Access Token 认证，并亲手走了一遍
  「令牌泄露 → 立即撤销 → 换新令牌」

## 踩过的两个坑

**1. Windows 原生 TLS 用不了**

Git 默认走 Windows 的系统 TLS，在受限环境里拿不到凭证，报：

```
schannel: AcquireCredentialsHandle failed: SEC_E_NO_CREDENTIALS
```

解决办法：改用 Git 自带的 OpenSSL。

```bash
git config --global http.sslBackend openssl
```

**2. 交互式提示弹不出来**

Git 要求输入用户名/密码时，会先在自己的临时目录写一个协调文件；受限环境拒绝写入，于是报
`could not read Username for 'https://github.com'`，提示永远出不来。

解决办法：不要让 Git 去问，而是**提前把凭据交给它**——用隐藏输入脚本喂令牌，
或让凭据管理器预先保存。

```bash
git config --global credential.helper wincred   # 加密存进 Windows 凭据管理器
```

