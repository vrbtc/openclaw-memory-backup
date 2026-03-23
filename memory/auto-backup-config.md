# 重大变更前自动备份提醒

**配置时间**: 2026-03-02 23:11
**状态**: ✅ 已配置

---

## 📋 备份策略

### 1. 每 6 小时自动备份
- **时间**: 00:00, 06:00, 12:00, 18:00
- **任务名**: OpenClaw Auto Backup
- **状态**: ✅ 已配置

### 2. 每天下午 2 点自动备份
- **时间**: 14:00
- **任务名**: OpenClaw Auto Backup
- **状态**: ✅ 已配置

### 3. 重大变更前手动备份
- **触发**: 用户准备修改重要配置前
- **命令**: `.\scripts\auto-backup.ps1`
- **状态**: ✅ 脚本已准备

---

## 🔧 配置详情

### 任务计划程序
| 项目 | 配置 |
|------|------|
| **任务名** | OpenClaw Auto Backup |
| **执行账户** | SYSTEM (最高权限) |
| **脚本路径** | `workspace/scripts/auto-backup.ps1` |
| **备份目录** | `C:\Users\Administrator\openclaw-backups\` |
| **保留策略** | 最近 7 个备份 |

### 触发器
1. **每 6 小时**: 重复间隔 6 小时
2. **每天 14:00**: 下午 2 点

---

## 📁 备份内容

**包含**:
- ✅ openclaw.json (主配置)
- ✅ .env (API Keys)
- ✅ workspace/ (工作目录)
- ✅ agents/ (代理配置)
- ✅ skills/ (已安装技能)
- ✅ memory/ (记忆文件)
- ✅ MEMORY.md (长期记忆)

**排除**:
- ❌ completions/ (缓存)
- ❌ *.log (日志文件)
- ❌ node_modules/ (依赖)
- ❌ .git/ (版本控制)

---

## 🎯 使用方法

### 查看下次备份时间
```powershell
Get-ScheduledTask -TaskName "OpenClaw Auto Backup" | Get-ScheduledTaskInfo
```

### 手动触发备份
```powershell
powershell -ExecutionPolicy Bypass -File "C:\Users\Administrator\.openclaw\workspace\scripts\auto-backup.ps1"
```

### 查看备份历史
```powershell
Get-ChildItem C:\Users\Administrator\openclaw-backups | Sort-Object LastWriteTime -Descending
```

### 恢复备份
```powershell
# 解压备份文件
Expand-Archive -Path "openclaw-2026-03-02_2227.zip" -DestinationPath "~\.openclaw"
```

---

## ⚠️ 注意事项

1. **重大变更前**: 修改配置前手动备份一次
2. **备份验证**: 定期测试备份文件可恢复性
3. **存储空间**: 监控备份目录大小
4. **网关状态**: 恢复前建议停止网关服务

---

_配置完成 | 2026-03-02 23:11 | 豆花 ⚡_
