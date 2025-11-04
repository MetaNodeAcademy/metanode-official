# GitHub Actions 部署到七牛云配置说明

本配置使用七牛云官方工具 `qshell` 进行文件上传部署。

## 配置步骤

### 1. 在 GitHub 仓库中设置 Secrets

在 GitHub 仓库设置 → Secrets and variables → Actions 中添加以下 Secrets：

- `QINIU_ACCESS_KEY`: 七牛云的 Access Key
- `QINIU_SECRET_KEY`: 七牛云的 Secret Key  
- `QINIU_BUCKET`: 七牛云存储空间名称
- `QINIU_CDN_URL` (可选): CDN 刷新 URL，格式如：`https://your-domain.com/*`

### 2. 自定义配置（可选）

如果需要修改上传行为，可以编辑 `.github/workflows/deploy-to-qiniu-simple.yml` 文件：

- `--key-prefix`: 文件上传的前缀路径（如果需要上传到子目录）
- `--ignore-dir`: 需要忽略的目录，用逗号分隔
- `--ignore-suffixes`: 需要忽略的文件后缀，用逗号分隔

### 3. 触发部署

- **自动触发**: 当代码推送到 `main` 分支时会自动触发部署
- **手动触发**: 在 GitHub Actions 页面可以手动触发工作流

## 工作流程

1. 检出代码
2. 下载并安装 qshell 工具
3. 配置 qshell 使用你的 Access Key 和 Secret Key
4. 上传文件到七牛云存储空间
5. （可选）刷新 CDN 缓存

## 注意事项

1. 确保七牛云存储空间已创建并配置好
2. 确保 Access Key 和 Secret Key 有足够的权限
3. 如果使用 CDN，需要配置 `QINIU_CDN_URL` secret
4. 默认会忽略 `.git`、`.github`、`node_modules` 目录和 `.md`、`.log` 文件

