# 🚀 TrendRadar 部署指南

本文档将详细说明如何部署 TrendRadar 项目，特别是如何配置 GitHub Pages。

---

## 📋 目录

1. [GitHub Pages 部署（网页版）](#github-pages-部署网页版)
2. [GitHub Actions 自动运行配置](#github-actions-自动运行配置)
3. [常见问题解答](#常见问题解答)

---

## 🌐 GitHub Pages 部署（网页版）

GitHub Pages 可以让你免费托管一个静态网站，访问地址格式为：`https://你的用户名.github.io/仓库名`

### 第一步：Fork 项目

1. 访问项目主页：https://github.com/sansan0/TrendRadar
2. 点击右上角的 **"Fork"** 按钮
3. 等待 Fork 完成，你会拥有一个属于自己的副本

### 第二步：配置 GitHub Pages

1. **进入你的 Fork 仓库**
   - 在 GitHub 上打开你 Fork 后的仓库

2. **打开设置页面**
   - 点击仓库顶部的 **"Settings"**（设置）标签
   - 在左侧菜单中找到 **"Pages"**（页面）选项

3. **启用 GitHub Pages**
   - 在 **"Source"**（源）部分，选择 **"Deploy from a branch"**（从分支部署）
   - 在 **"Branch"**（分支）下拉菜单中：
     - 选择 **"main"** 或 **"master"**（根据你的默认分支名称）
     - 选择 **"/ (root)"**（根目录）
   - 点击 **"Save"**（保存）按钮

   ⚠️ **如果 Save 按钮是灰色的，无法点击，请检查以下几点：**
   
   **问题 1：没有选择分支和目录**
   - 确保两个下拉菜单都已选择：
     - 第一个下拉菜单：选择分支（`main` 或 `master`）
     - 第二个下拉菜单：选择目录（`/ (root)`）
   - 只有两个都选择后，Save 按钮才会变为可点击状态
   
   **问题 2：找不到分支选项**
   - 如果下拉菜单中没有分支选项，可能是仓库还没有内容
   - 确保你已经成功 Fork 了项目
   - 刷新页面重试
   
   **问题 3：权限问题**
   - 确保你是仓库的所有者（Fork 后你就是所有者）
   - 如果是从组织 Fork 的，可能需要组织管理员权限

4. **获取你的 GitHub Pages 地址**
   - 保存后，GitHub 会显示你的网站地址
   - 格式通常是：`https://你的用户名.github.io/TrendRadar`
   - ⚠️ **注意**：首次启用可能需要几分钟才能生效

### 第三步：修改配置文件

1. **编辑配置文件**
   - 在你的仓库中，找到 `config/config.yaml` 文件
   - 点击文件，然后点击右上角的 **"✏️ Edit"**（编辑）按钮

2. **修改 base_url**
   - 找到 `app` 部分的 `base_url` 配置
   - 将默认值替换为你的 GitHub Pages 地址
   
   ```yaml
   app:
     # 将下面的 URL 替换为您自己的 GitHub Pages 地址
     base_url: "https://你的用户名.github.io/TrendRadar"
   ```

   **示例**：
   ```yaml
   app:
     base_url: "https://joyce677.github.io/TrendRadar"
   ```

3. **保存更改**
   - 滚动到页面底部
   - 填写提交信息（如："配置 GitHub Pages 地址"）
   - 点击 **"Commit changes"**（提交更改）

### 第四步：配置关键词（可选但推荐）

1. **编辑关键词文件**
   - 找到 `config/frequency_words.txt` 文件
   - 点击编辑，添加你关心的关键词

2. **关键词配置示例**
   ```
   人工智能
   AI
   ChatGPT
   +技术
   !广告
   ```

   详细配置说明请参考 README.md 中的 `frequency_words.txt 配置教程` 部分

### 第五步：等待自动运行

1. **GitHub Actions 会自动运行**
   - 项目配置了每小时自动运行一次（整点执行）
   - 你也可以手动触发：
     - 进入仓库的 **"Actions"**（操作）标签
     - 选择 **"Hot News Crawler"** 工作流
     - 点击 **"Run workflow"**（运行工作流）按钮

2. **查看运行结果**
   - 运行完成后，会自动生成 `index.html` 文件
   - 访问你的 GitHub Pages 地址即可查看热点新闻

---

## ⚙️ GitHub Actions 自动运行配置

### 工作原理

项目使用 GitHub Actions 自动执行爬虫任务：
- **运行频率**：默认每小时整点运行一次
- **执行内容**：
  1. 爬取各大平台热点新闻
  2. 根据关键词筛选新闻
  3. 生成 HTML 报告
  4. 自动提交到仓库（更新 `index.html`）

### 查看运行状态

1. **进入 Actions 页面**
   - 在你的仓库中，点击顶部的 **"Actions"** 标签

2. **查看运行历史**
   - 左侧显示所有工作流
   - 右侧显示每次运行的详细信息
   - 绿色 ✅ 表示成功，红色 ❌ 表示失败

3. **查看运行日志**
   - 点击任意一次运行记录
   - 可以查看详细的执行日志
   - 如果失败，日志会显示错误原因

### 手动触发运行

如果不想等待自动运行，可以手动触发：

1. 进入 **"Actions"** 标签
2. 选择 **"Hot News Crawler"** 工作流
3. 点击右侧的 **"Run workflow"** 按钮
4. 选择分支（通常是 `main`）
5. 点击 **"Run workflow"** 确认

---

## 🔔 配置手机推送通知（可选）

如果你希望收到手机推送通知，需要配置相应的机器人。详细步骤请参考 README.md 中的相关章节。

### 支持的推送平台

- **企业微信**（推荐，配置最简单）
- **飞书**（显示效果最佳）
- **钉钉**
- **Telegram**

### 配置步骤（以企业微信为例）

1. **创建企业微信机器人**
   - 打开企业微信 App → 进入目标群聊
   - 点击右上角"…" → 选择"群机器人"
   - 点击"添加" → 设置机器人昵称
   - 复制 Webhook 地址

2. **配置 GitHub Secrets**
   - 进入仓库的 **"Settings"** → **"Secrets and variables"** → **"Actions"**
   - 点击 **"New repository secret"**
   - 名称填写：`WEWORK_WEBHOOK_URL`
   - 值填写：你复制的 Webhook 地址
   - 点击 **"Add secret"** 保存

3. **完成**
   - 下次 GitHub Actions 运行时，会自动发送通知到你的企业微信群

---

## ❓ 常见问题解答

### Q1: GitHub Pages 设置页面中 Save 按钮是灰色的，无法点击？

**这是最常见的问题！** 解决方法如下：

1. **检查是否选择了分支和目录**
   - 在 "Source" 部分，你需要选择两个下拉菜单：
     - **第一个下拉菜单**：选择分支（通常是 `main` 或 `master`）
     - **第二个下拉菜单**：选择目录（选择 `/ (root)`）
   - **重要**：只有两个下拉菜单都选择后，Save 按钮才会变为可点击状态（从灰色变为绿色/蓝色）

2. **操作步骤**：
   ```
   步骤 1：点击 "Source" 下的第一个下拉菜单 → 选择 "main" 或 "master"
   步骤 2：点击第二个下拉菜单 → 选择 "/ (root)"
   步骤 3：此时 Save 按钮应该变为可点击状态
   步骤 4：点击 Save 按钮保存
   ```

3. **如果仍然无法选择**：
   - 刷新页面重试
   - 确保你已经成功 Fork 了项目
   - 检查仓库中是否有文件（Fork 后应该自动包含所有文件）

4. **截图参考**：
   - 正确的配置应该显示：
     ```
     Source: Deploy from a branch
     Branch: main ──────────┐
                            │ 这两个都要选择！
     Folder: / (root) ──────┘
     ```

### Q2: GitHub Pages 显示 404 错误？

**可能原因和解决方法：**

1. **GitHub Pages 还未生效**
   - 首次启用后需要等待 5-10 分钟
   - 刷新页面重试

2. **分支或目录配置错误**
   - 检查 Settings → Pages 中的配置
   - 确保选择的是 `main` 分支和 `/ (root)` 目录

3. **index.html 文件不存在**
   - 等待 GitHub Actions 运行一次
   - 或者手动触发一次运行

### Q3: 如何修改运行频率？

编辑 `.github/workflows/crawler.yml` 文件：

```yaml
on:
  schedule:
    - cron: "0 * * * *"  # 每小时整点运行
```

常用 cron 表达式：
- `"0 * * * *"` - 每小时整点
- `"*/30 * * * *"` - 每 30 分钟
- `"0 9,12,18 * * *"` - 每天 9点、12点、18点

⚠️ **注意**：GitHub 免费账户有资源限制，不建议设置过于频繁的运行。

### Q4: 如何更新项目到最新版本？

**小版本更新**：
- 直接在 GitHub 网页编辑器中，用原项目的 `main.py` 代码替换你仓库中的对应文件

**大版本升级**：
- 建议删除现有 fork 后重新 fork，避免配置冲突

### Q5: 如何自定义域名？

1. 在仓库根目录创建 `CNAME` 文件
2. 文件内容填写你的域名，例如：`news.example.com`
3. 在你的域名 DNS 设置中添加 CNAME 记录，指向 `你的用户名.github.io`
4. 等待 DNS 生效（通常需要几分钟到几小时）

### Q6: GitHub Actions 运行失败怎么办？

1. **查看错误日志**
   - 进入 Actions 页面，查看失败的运行记录
   - 查看详细的错误信息

2. **常见错误**

   **错误 1：推送被拒绝（fetch first）**
   ```
   error: failed to push some refs
   Updates were rejected because the remote contains work that you do not have locally
   ```
   **原因**：远程仓库有新的提交（可能是手动提交或其他运行）
   **解决方法**：
   - 项目已更新工作流配置，会自动处理这种情况
   - 如果仍然失败，可以手动拉取远程更改：
     ```bash
     git pull --rebase origin main
     ```
   - 或者等待下次自动运行，会自动处理

   **错误 2：配置文件缺失**
   - 确保 `config/config.yaml` 和 `config/frequency_words.txt` 存在
   - 检查文件路径是否正确

   **错误 3：依赖安装失败**
   - 通常是网络问题，重试即可
   - 或者等待 GitHub Actions 服务器恢复

   **错误 4：权限问题**
   - 确保仓库设置中允许 Actions 写入
   - 检查 Settings → Actions → General → Workflow permissions

3. **重新运行**
   - 点击失败的运行记录
   - 点击右上角的 **"Re-run jobs"** 按钮

### Q7: 如何查看生成的报告文件？

生成的报告文件保存在以下位置：

- **网页版**：`index.html`（根目录，GitHub Pages 入口）
- **历史记录**：`output/YYYY-MM-DD/html/` 目录下
- **文本报告**：`output/YYYY-MM-DD/txt/` 目录下

### Q8: 如何修改监控的平台？

编辑 `config/config.yaml` 文件中的 `platforms` 部分：

```yaml
platforms:
  - id: "toutiao"
    name: "今日头条"
  - id: "baidu"
    name: "百度热搜"
  # 添加更多平台...
```

可用的平台 ID 请参考 [newsnow 项目](https://github.com/ourongxing/newsnow) 的源代码。

### Q9: 钉钉机器人配置了但没有发送通知？

**钉钉机器人常见问题和解决方法：**

1. **检查 GitHub Secrets 配置**
   - 进入仓库的 **"Settings"** → **"Secrets and variables"** → **"Actions"**
   - 确认是否有名为 `DINGTALK_WEBHOOK_URL` 的 Secret（注意大小写）
   - 确认 Secret 的值是完整的 webhook URL（格式类似：`https://oapi.dingtalk.com/robot/send?access_token=xxx`）

2. **钉钉机器人安全设置（最重要！）**
   
   ⚠️ **重要提示**：本项目**只支持"自定义关键词"方式，不支持"加签"方式**
   
   **必须使用"自定义关键词"安全设置：**
   - 钉钉机器人**必须**设置"自定义关键词"安全设置
   - 关键词必须设置为：**"热点"**
   - 如果使用"加签"方式，会提示"签名不匹配"错误
   
   **检查/修改步骤**：
   1. 打开钉钉 PC 客户端
   2. 进入机器人所在的群聊
   3. 点击群设置图标（⚙️）→ 找到"机器人"
   4. 找到你的机器人 → 点击"设置"
   5. 查看"安全设置"
   6. **如果显示"加签"**：
      - 需要删除当前机器人，重新创建一个
      - 创建时选择"自定义关键词"方式
      - 关键词设置为：**"热点"**
   7. **如果显示"自定义关键词"**：
      - 确认关键词中包含了"热点"
      - 如果没有，点击"编辑"添加"热点"
   
   **重新创建机器人步骤**（如果当前使用的是加签）：
   1. 删除当前的机器人
   2. 点击"添加机器人" → "自定义"
   3. 设置机器人名称
   4. **安全设置**：选择 **"自定义关键词"**
   5. 关键词填写：**"热点"**
   6. 勾选服务条款 → 点击"完成"
   7. 复制新的 Webhook URL
   8. 更新 GitHub Secrets 中的 `DINGTALK_WEBHOOK_URL`

3. **查看运行日志确认错误（详细步骤）**
   
   **步骤 1：进入 Actions 页面**
   - 在你的 GitHub 仓库页面，点击顶部的 **"Actions"** 标签
   
   **步骤 2：找到运行记录**
   - 左侧会显示工作流列表，选择 **"Hot News Crawler"**
   - 右侧会显示运行历史记录（按时间倒序）
   - 找到最新的运行记录（通常在最上面）
   - 点击运行记录进入详情页
   
   **步骤 3：查看详细日志**
   - 在运行详情页，你会看到多个步骤（steps）
   - 找到 **"Run crawler"** 这一步（这是执行爬虫的步骤）
   - 点击 **"Run crawler"** 展开日志
   - 日志会显示所有输出信息
   
   **步骤 4：搜索关键信息**
   - 在日志中按 `Ctrl+F`（Windows）或 `Cmd+F`（Mac）搜索关键词：
     - 搜索 **"钉钉"** - 找到钉钉相关的日志
     - 搜索 **"webhook"** - 查看 webhook 配置信息
     - 搜索 **"错误"** 或 **"失败"** - 找到错误信息
     - 搜索 **"通知"** - 查看通知发送情况
   
   **步骤 5：查看关键日志行**
   - 查找包含以下内容的日志行：
     - `钉钉(环境变量)` 或 `钉钉(配置文件)` - 说明读取了 webhook 配置
     - `钉钉通知发送成功` - 说明发送成功
     - `钉钉通知发送失败` - 会显示具体错误信息
     - `钉钉通知发送出错` - 会显示异常信息
     - `未配置任何webhook URL` - 说明没有读取到配置
   
   **常见错误信息**：
   - `机器人发送签名不匹配` - **你使用了"加签"方式，需要改用"自定义关键词"方式**
   - `errcode: 310000` 或 `关键词不匹配` - 需要设置关键词"热点"
   - `errcode: 300001` - webhook URL 无效
   - `状态码：403` - 权限问题或安全设置问题
   - `状态码：404` - webhook URL 不存在或已失效
   
   **如果看不到日志**：
   - 确认运行是否已完成（等待运行完成）
   - 如果运行失败（红色❌），点击查看失败原因
   - 如果运行还在进行中（黄色🟡），等待完成

4. **确认 webhook URL 格式**
   - 正确的格式：`https://oapi.dingtalk.com/robot/send?access_token=xxxxxxxxxx`
   - 确保 URL 完整，没有多余的空格或换行
   - 确保 access_token 正确

5. **测试 webhook URL**
   - 可以使用 curl 命令测试（在本地终端）：
   ```bash
   curl -X POST "你的webhook地址" \
   -H "Content-Type: application/json" \
   -d '{"msgtype":"text","text":{"content":"测试消息"}}'
   ```
   - 如果返回 `{"errcode":0,"errmsg":"ok"}` 说明配置正确
   - 如果返回错误，根据错误码排查问题

6. **确认有匹配的新闻**
   - 如果关键词配置太严格，可能没有匹配到任何新闻
   - 查看运行日志，确认是否有匹配的新闻
   - 可以先测试一些常见关键词（如"中国"、"美国"）

7. **检查通知功能是否启用**
   - 确认 `config/config.yaml` 中 `enable_notification: true`

**快速排查步骤：**
```
1. ✅ 检查 GitHub Secrets 中是否有 DINGTALK_WEBHOOK_URL
2. ✅ 确认钉钉机器人安全设置中关键词包含"热点"
3. ✅ 查看 Actions 运行日志，找到钉钉相关的错误信息
4. ✅ 测试 webhook URL 是否有效
5. ✅ 确认有匹配的新闻
```

### Q10: 机器人没有发送通知消息？

**可能的原因和解决方法：**

1. **没有配置 GitHub Secrets（最常见）**
   - 检查是否在 GitHub 仓库中配置了机器人的 webhook
   - 进入仓库的 **"Settings"** → **"Secrets and variables"** → **"Actions"**
   - 查看是否有配置以下任一 Secret：
     - `WEWORK_WEBHOOK_URL`（企业微信）
     - `FEISHU_WEBHOOK_URL`（飞书）
     - `DINGTALK_WEBHOOK_URL`（钉钉）
     - `TELEGRAM_BOT_TOKEN` 和 `TELEGRAM_CHAT_ID`（Telegram）
   - **如果没有配置，需要先创建机器人并配置 Secret**（参考 README.md 中的详细步骤）

2. **通知功能被关闭**
   - 检查 `config/config.yaml` 文件
   - 确认 `enable_notification: true`（不是 `false`）

3. **没有匹配到新闻**
   - 如果关键词配置太严格，可能没有匹配到任何新闻
   - 查看 GitHub Actions 运行日志，确认是否有匹配的新闻
   - 可以先测试一些常见关键词（如"中国"、"美国"）验证配置是否正确

4. **静默推送模式开启**
   - 检查 `config/config.yaml` 中的 `silent_push.enabled`
   - 如果为 `true`，只在指定时间范围内推送
   - 检查当前时间是否在推送时间范围内

5. **增量模式且没有新增新闻**
   - 如果 `report.mode` 设置为 `incremental`
   - 只有在有新出现的匹配新闻时才会推送
   - 可以改为 `daily` 模式测试

6. **查看运行日志**
   - 进入 **"Actions"** 页面，查看最新的运行记录
   - 点击运行记录，查看详细日志
   - 日志中会显示：
     - 是否读取了 webhook 配置
     - 匹配了多少条新闻
     - 是否发送了通知
     - 如果有错误，会显示错误信息

**快速排查步骤：**
```
1. ✅ 检查 GitHub Secrets 是否配置
2. ✅ 检查 config.yaml 中 enable_notification 是否为 true
3. ✅ 查看 Actions 运行日志，确认是否有匹配的新闻
4. ✅ 检查静默推送模式是否开启
5. ✅ 确认运行时间是否在推送时间范围内
```

### Q11: 修改了 frequency_words.txt 但没有看到效果？

**这是最常见的问题！** 修改关键词后不会立即生效，需要等待 GitHub Actions 运行。

**解决方法：**

1. **手动触发 GitHub Actions 运行**
   - 进入仓库的 **"Actions"** 标签
   - 选择 **"Hot News Crawler"** 工作流
   - 点击右侧的 **"Run workflow"** 按钮
   - 选择分支（通常是 `main`）
   - 点击 **"Run workflow"** 确认
   - 等待运行完成（通常需要 2-5 分钟）

2. **检查关键词配置格式**
   - 确保关键词之间用**空行**分隔不同的词组
   - 每行一个关键词
   - 使用 `+关键词` 表示必须词
   - 使用 `!关键词` 表示过滤词

   **正确示例：**
   ```
   人工智能
   AI
   ChatGPT
   
   谷歌
   google
   gemini
   ```

   **错误示例：**
   ```
   人工智能 AI ChatGPT  # ❌ 错误：多个词在一行
   谷歌 google gemini    # ❌ 错误：没有用空行分隔词组
   ```

3. **检查关键词是否匹配**
   - 关键词匹配是**不区分大小写**的
   - 关键词只要**包含**在新闻标题中就会匹配
   - 例如：关键词 "AI" 会匹配标题 "OpenAI发布新模型"

4. **查看运行日志**
   - 进入 Actions 页面，查看最新的运行记录
   - 点击运行记录，查看日志输出
   - 日志中会显示：
     - 读取了多少个标题
     - 匹配了多少个关键词
     - 生成了多少条热点新闻

5. **确认配置文件已保存**
   - 确保你在 GitHub 网页上编辑并保存了文件
   - 或者通过 Git 提交了更改
   - 检查文件内容是否正确（点击文件查看）

6. **等待自动运行**
   - 如果不想手动触发，可以等待下一次自动运行
   - 默认每小时整点运行一次
   - 运行完成后会自动更新 `index.html` 文件

**排查步骤总结：**
```
1. ✅ 修改了 frequency_words.txt 并保存
2. ✅ 手动触发 GitHub Actions 运行（或等待自动运行）
3. ✅ 查看运行日志，确认关键词被正确读取
4. ✅ 等待运行完成（2-5分钟）
5. ✅ 刷新 GitHub Pages 页面查看效果
```

**如果仍然没有效果：**
- 检查关键词拼写是否正确
- 确认关键词确实出现在新闻标题中（可以先测试一些常见词，如"中国"、"美国"）
- 查看运行日志中的错误信息
- 确认 `config/config.yaml` 中的 `report.mode` 设置正确

---

## 📝 总结

完成以上步骤后，你的 TrendRadar 项目就部署完成了！

**部署检查清单**：
- [ ] Fork 了项目
- [ ] 启用了 GitHub Pages
- [ ] 修改了 `config/config.yaml` 中的 `base_url`
- [ ] 配置了关键词（可选）
- [ ] 等待 GitHub Actions 运行一次
- [ ] 访问 GitHub Pages 地址查看效果

**下一步**：
- 配置手机推送通知（可选）
- 根据需求调整关键词和运行模式
- 享受精准的热点新闻推送！

如有问题，欢迎在项目 Issues 中提问。

