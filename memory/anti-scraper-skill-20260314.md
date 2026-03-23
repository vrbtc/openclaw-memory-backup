# 反爬网页访问技能固化记录

**固化时间**: 2026-03-14 20:02  
**触发原因**: 微信文章被反爬，老板指令学习反爬技能  
**老板指令**: "请学会反爬网页访问技能"

---

## ✅ 已创建文件

| 文件 | 用途 |
|------|------|
| `scripts/anti_scraper.py` | 反爬网页访问脚本 |
| `logs/web_scraper.log` | 抓取日志 |

---

## 🔧 方法优先级（固化）

### 方法 1: curl + 移动端 UA ⭐（最快）
```python
User-Agent: Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X)
```
**优点**:
- ✅ 速度快（1-3 秒）
- ✅ 绕过大部分反爬
- ✅ 无需额外依赖

**测试结果**: ✅ 成功抓取微信文章（2.7MB）

---

### 方法 2: r.jina.ai API
```
https://r.jina.ai/URL
```
**优点**:
- ✅ 绕过 Cloudflare
- ✅ 返回 Markdown 格式
- ✅ 免费使用

**缺点**:
- ⚠️ 微信文章仍可能返回验证码

---

### 方法 3: Chrome Headless dump-dom
```bash
chrome.exe --headless --dump-dom --no-sandbox URL
```
**优点**:
- ✅ 完整 JS 渲染
- ✅ 绕过 JS 反爬

**缺点**:
- ⚠️ 速度较慢（5-10 秒）
- ⚠️ 需要 Chrome 浏览器

---

### 方法 4: Chrome Remote Debugging
```bash
chrome.exe --remote-debugging-port=9222
```
**优点**:
- ✅ 最强反爬绕过
- ✅ 可模拟真人操作

**缺点**:
- ⚠️ 配置复杂
- ⚠️ 需要额外端口

---

## 📱 微信公众号专用

### 抓取命令
```bash
curl -s -A 'Mozilla/5.0 (iPhone...)' 'URL' > page.html
```

### 内容提取
```python
# 提取 id="js_content" 内容
match = re.search(r'<div[^>]*id="js_content"[^>]*>(.*?)</div>', html, re.DOTALL)
```

---

## 🧪 测试结果

| 网站 | 方法 1 | 方法 2 | 方法 3 |
|------|--------|--------|--------|
| 微信公众号 | ✅ 成功 | ❌ 验证码 | ⏳ 未测试 |
| 一般网站 | ✅ 成功 | ✅ 成功 | ✅ 成功 |
| Cloudflare | ⚠️ 可能失败 | ✅ 成功 | ✅ 成功 |

---

## 📝 使用示例

### 命令行
```bash
python anti_scraper.py https://mp.weixin.qq.com/s/xxx
```

### Python 调用
```python
from anti_scraper import scrape_url

content, method = scrape_url("https://example.com")
print(f"使用 {method} 方法抓取成功")
```

---

## ⚠️ 注意事项

1. **按顺序尝试** - 先用方法 1，失败再用方法 2，以此类推
2. **全部失败才报告** - 不要第一个方法失败就放弃
3. **日志记录** - 每次抓取都记录到 `logs/web_scraper.log`
4. **代理配置** - 需要时配置 `PROXY = "http://127.0.0.1:7890"`

---

## 🎯 下次自动使用

**微信文章抓取流程**:
1. 调用 `anti_scraper.py`
2. 自动按优先级尝试 4 种方法
3. 提取 `js_content` 内容
4. 推送总结到飞书

---

**固化完成！以后遇到反爬网站自动使用这些方法！** ✅

_监督者：老板（润）_  
_执行者：总指挥 → 进化官_  
_状态：已固化_
