# 天气查询技能固化记录

**固化时间**: 2026-03-14 19:50  
**触发原因**: 天气晚报 API 失败，改用 Open-Meteo 成功  
**老板指令**: "固化这个技能调用方法，下次每次查天气和每次的天气通知提醒推送必须用这个查"

---

## ✅ 固化的 API

| 项目 | 配置 |
|------|------|
| **API 名称** | Open-Meteo Weather API |
| **API 地址** | `https://api.open-meteo.com/v1/forecast` |
| **文档** | https://open-meteo.com/en/docs |
| **费用** | 完全免费 |
| **API Key** | 不需要 |
| **更新频率** | 每小时更新 |

---

## 📍 坐标配置

| 城市 | 纬度 | 经度 |
|------|------|------|
| **西安** | 34.3416 | 108.9398 |

---

## 🔧 修改的文件

**文件**: `C:\Users\Administrator\.openclaw\workspace\scripts\weather_report.py`

**修改内容**:
1. ✅ 添加 API 固化说明注释
2. ✅ 完善天气代码映射（WMO 代码）
3. ✅ 添加详细日志输出
4. ✅ 增加超时时间（15 秒）
5. ✅ 添加网络错误处理

---

## 🌤️ 天气代码映射

| 代码 | 天气 | 图标 |
|------|------|------|
| 0 | 晴天 | ☀️ |
| 1-3 | 晴间多云/多云/阴天 | 🌤️⛅☁️ |
| 45-48 | 雾/霾 | 🌫️ |
| 51-67 | 各种降雨 | 🌦️🌧️🌨️ |
| 71-86 | 各种降雪 | 🌨️❄️ |
| 80-82 | 阵雨 - 暴雨 | 🌦️🌧️⛈️ |
| 95-99 | 雷暴 | ⛈️ |

---

## 📋 推送规则

### 早报（07:00）
- ✅ 当前天气
- ✅ 今天最高/最低温
- ✅ 今天天气趋势
- ✅ 降水概率
- ✅ 生活建议

### 晚报（18:00）
- ✅ 当前天气
- ⚠️ **异常天气才推送**（下雨/下雪/雷暴等）
- ✅ 未来 6 小时预报
- ✅ 夜间温度

---

## 🔍 异常天气定义

以下天气代码触发推送：

```python
ABNORMAL_CODES = [
    45, 48,  # 雾/霾
    51, 53, 55, 56, 57,  # 各种降雨
    61, 63, 65, 66, 67,  # 各种降雨
    71, 73, 75, 77,  # 各种降雪
    80, 81, 82,  # 阵雨 - 暴雨
    85, 86,  # 阵雪
    95, 96, 99  # 雷暴
]
```

---

## 📊 API 调用示例

### 请求 URL
```
https://api.open-meteo.com/v1/forecast?
latitude=34.3416&longitude=108.9398
&current_weather=true
&hourly=temperature_2m,precipitation,weather_code
&timezone=Asia/Shanghai
&forecast_days=3
```

### 返回数据
```json
{
  "current_weather": {
    "temperature": 4.2,
    "weathercode": 61,
    "windspeed": 11.4,
    "is_day": 0
  },
  "hourly": {
    "temperature_2m": [...],
    "precipitation": [...],
    "weather_code": [...]
  }
}
```

---

## ✅ 验证方法

### 手动测试
```bash
C:\Users\Administrator\AppData\Local\Programs\Python\Python311\python.exe C:\Users\Administrator\.openclaw\workspace\scripts\weather_report.py --type evening
```

### 查看日志
```
C:\Users\Administrator\.openclaw\workspace\logs\weather_report.log
```

---

## 📝 定时任务

| 任务 | 时间 | 脚本 |
|------|------|------|
| **天气早报** | 07:00 | `weather_report.py --type morning` |
| **天气晚报** | 18:00 | `weather_report.py --type evening` |

---

## ⚠️ 注意事项

1. **必须使用 Open-Meteo API** - 不要换成其他天气 API
2. **免费无需 Key** - 不用担心配额限制
3. **每小时更新** - 数据时效性好
4. **全球覆盖** - 可以切换城市坐标

---

**固化完成！以后所有天气查询和推送都必须使用 Open-Meteo API！** ✅

_监督者：老板（润）_  
_执行者：总指挥 → 进化官_  
_状态：已固化_
