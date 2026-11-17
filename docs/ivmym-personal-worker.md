# IVMYM fork — personal Worker 与快捷指令

本 fork 不修改上游公共实例 `https://wloc-spoofer.wloc.workers.dev/`。自部署时使用独立 Worker 名称，避免覆盖他人服务。

## 构建与测试

```bash
cd worker
npm install
npm test
```

## 部署（需本机或 CI 的 `CLOUDFLARE_API_TOKEN`）

```bash
cd worker
npx wrangler deploy -c wrangler.personal.jsonc --minify
```

配置要点（与上游一致）：

- `compatibility_date`: `2026-08-05`
- `observability.enabled`: `false`
- 无 KV / D1 / 环境变量绑定

本地仅打包、不上传：

```bash
npx wrangler deploy -c wrangler.personal.jsonc --minify --dry-run --outdir=../artifacts/wrangler-out
```

## 快捷指令

官方快捷指令为 iCloud 公开链接（见根目录 `README.md`），**解析链接**的一步会请求：

`https://wloc-spoofer.wloc.workers.dev/api/parse`

**只有在你自己的 Worker 部署成功并得到真实 `*.workers.dev`（或自定义域）后**，在「副本」快捷指令里把主机名换成你的域名；**路径 `/api/parse` 与动作逻辑保持不变**。

操作步骤：

1. 从 README 中的 iCloud 链接「添加快捷指令」到资料库（得到私有副本）。
2. 编辑 **wloc 设置地理位置**，定位含 `wloc-spoofer.wloc.workers.dev` 的 URL 动作，仅改主机名。
3. 勿修改公共 iCloud 分享页；勿将改过的快捷指令重新发布为第三方公共链接。

`.shortcut` 为 Apple 专有二进制/归档格式，本仓库**不**附带可导入成品；需要从设备「导出」或由用户在快捷指令 App 内按上述步骤修改。

## Cloud Agent 产物

在具备 token 的环境外，Agent 可在 `/opt/cursor/artifacts/wloc-ivmym-deploy/` 生成单文件 `index.js` + `wrangler.personal.jsonc` + `metadata.json` 供授权工具上传。