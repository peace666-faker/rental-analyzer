# 🏠 租房避雷 —— Claude Code 智能租房分析 Skill

> 算钱 · 找硬伤 · 看退路 —— 不打无准备之仗

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 这个 Skill 做什么

在 Claude Code 中输入 `/rental-analyzer`，上传房源信息，它会帮你**避雷**：

- **算钱** —— 全口径月支出（含隐性成本），房租占比评估
- **找硬伤** —— 一票否决项（隔断 / 发霉 / 朝北 / 商用天价电 / 没房产证）
- **看退路** —— 转租好不好出手？合同卡不卡？打工人多不多？
- **给框架** —— 老小区 vs 新、整租 vs 合租、短租 vs 长租

附带一份 **8 项实地看房速查清单**。

## 安装

### 全局安装（推荐）

```bash
# 创建全局 skills 目录（如果还没有）
mkdir -p ~/.claude/skills

# 克隆本仓库
git clone https://github.com/peace666-faker/rental-analyzer.git /tmp/rental-analyzer

# 复制 skill 到全局目录
cp -r /tmp/rental-analyzer/.claude/skills/rental-analyzer ~/.claude/skills/

# 清理
rm -rf /tmp/rental-analyzer
```

### 项目级安装

```bash
# 在你的项目根目录
mkdir -p .claude/skills
cp -r /path/to/rental-analyzer/.claude/skills/rental-analyzer .claude/skills/
```

### 安装后

重启 Claude Code 会话，输入 `/rental-analyzer` 即可使用。

也可以直接说 "帮我分析一下这两套租房" —— Skill 会自动触发。

## 使用示例

```
/rental-analyzer

然后按提示输入：
- 城市、月租、面积、朝向、楼层
- 厨卫情况、通勤时间、月薪
- 做饭频率、小区类型

Skill 会输出完整分析报告。
```

## 适用人群

- 正在找房的打工人
- 在校生找实习/毕业租房
- 第一次租房不知道怎么选的人
- 想确认当前房子值不值得续租的人

## 特点

| 特性 | 说明 |
|------|------|
| 🌍 全国通用 | 自适应城市等级、物价、气候、商务区分布 |
| 👩 性别安全 | 按男女区分安保评估 |
| 💰 隐性成本 | 水电类型、家电能耗、物业网费、转租成本 |
| 🔄 转租视角 | 合同 + 同品质房源竞争度 |
| 🦠 避雷检查 | 隔断房 / 发霉 / 串串房 / 中介识别 |
| 🏙️ 城市提醒 | 南方防霉 / 北方问暖 / 小城市标准不同 |

## 文件结构

```
rental-analyzer/
├── .claude/
│   └── skills/
│       └── rental-analyzer/
│           └── SKILL.md          # Skill 定义文件
├── README.md
└── LICENSE
```

## License

MIT

## 作者

GitHub: [@peace666-faker](https://github.com/peace666-faker)
