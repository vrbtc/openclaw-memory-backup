# Capability Evolver 自我进化引擎

**安装时间**: 2026-03-15（已存在）  
**来源**: clawhub install evolver  
**位置**: `skills/evolver/`

---

## 🧬 功能

1. **自动日志分析** - 扫描记忆和历史文件找错误模式
2. **自我修复** - 检测崩溃并建议补丁
3. **GEP 协议** - 标准化进化流程（可复用资产）
4. **一键进化** - 运行 `/evolve` 或 `node index.js`

---

## 🔧 使用方法

### 自动运行
```bash
cd skills/evolver
node index.js
```

### 审查模式
```bash
node index.js --review
```

### 连续循环
```bash
node index.js --loop
```

---

## ⚙️ 配置

**环境变量**:
- `A2A_NODE_ID` - EvoMap 节点身份（必填）
- `EVOLVE_ALLOW_SELF_MODIFY=false` - 禁止修改自身源码
- `EVOLVE_STRATEGY=balanced` - 平衡策略

**本地覆盖**:
- `EVOLVE_REPORT_TOOL=feishu-card` - 使用飞书卡片报告

---

## 🛡️ 安全协议

1. **身份注入** - "你是递归自我改进系统"
2. **突变指令** - 有错误→修复模式，稳定→强制优化
3. **无限递归防护** - 严格单进程逻辑
4. **Git 同步** - 建议运行 git-sync cron

---

## 📊 使用场景

- 分析运行历史找能力短板
- 自动修复重复错误
- 优化低效流程
- 协议约束下安全进化

---

**监督者**: 老板（润）  
**状态**: 已安装待配置
