# claw123.ai 技能搜索方法

**固化时间**: 2026-03-15 03:30  
**来源**: 老板指令  
**技能总数**: 5,485 个

---

## 📚 搜索方法

### 步骤 1: 获取技能列表
```bash
curl -s -x "http://127.0.0.1:7890" "https://claw123.ai/api/skills.zh.json"
```

**返回字段**:
- `name`: 技能名
- `description_zh`: 中文描述
- `category_zh`: 中文分类
- `url`: 源地址（GitHub）

### 步骤 2: 搜索匹配技能
```python
# 按关键词搜索
skills = [s for s in skills_list if keyword in s['name'] or keyword in s['description_zh']]
```

### 步骤 3: 获取技能详情
```bash
# 读取技能的 SKILL.md
curl -s "https://raw.githubusercontent.com/..." > SKILL.md
```

### 步骤 4: 主人确认后安装
```bash
clawhub install <技能名>
```

---

## 🎯 使用原则

1. ✅ **按需查找** - 主人需要某个功能时才搜索
2. ✅ **主人确认** - 搜索到技能后先推荐给主人，确认后再安装
3. ✅ **不要一次性安装所有** - 避免技能臃肿
4. ✅ **优先 claw123.ai** - 5000+ 可信技能，优先这里查找

---

## 📊 技能分类（Top 10）

| 分类 | 数量 |
|------|------|
| Coding Agents & IDEs | 1,221 |
| Web & Frontend Development | 937 |
| DevOps & Cloud | 409 |
| Search & Research | 354 |
| Browser & Automation | 334 |
| Productivity & Tasks | 206 |
| AI & LLMs | 197 |
| CLI Utilities | 186 |
| Git & GitHub | 169 |
| Communication | 149 |

---

## 📝 使用示例

**场景**: 主人需要"机票查询"功能

1. 搜索 claw123.ai: `curl ... "https://claw123.ai/api/skills.zh.json"`
2. 过滤关键词: `机票` 或 `flight`
3. 找到技能: `flyclaw` - 航班信息聚合查询工具
4. 推荐给主人: "找到机票查询技能 flyclaw，支持单程/往返/价格日历，要安装吗？"
5. 主人确认后: `clawhub install flyclaw`

---

**监督者**: 老板（润）  
**状态**: 已固化待执行
