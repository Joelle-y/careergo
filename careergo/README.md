# CareerGo · 求职智能匹配与简历诊断平台

> 面向在校大学生和应届毕业生的 AI 求职辅助工具，帮助学生快速匹配合适岗位，并诊断简历与心仪岗位的差距。

## 技术栈

- **HTML5** — 单文件应用，无需构建
- **Tailwind CSS** (Play CDN) — 原子化 CSS 框架
- **Lucide Icons** — SVG 矢量图标库
- **Google Fonts** — Outfit (标题) + Work Sans (正文)
- **localStorage** — 模拟后端数据持久化
- **ui-ux-pro-max-skill** — 设计规范来源

## 设计规范

本项目使用 [ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) 生成设计系统，遵循以下规范：

### 视觉风格：玻璃拟态（Glassmorphism）

| 参数 | 值 |
|------|-----|
| 背景模糊 | `backdrop-filter: blur(20px)` |
| 半透明白色 | `rgba(255,255,255,0.15-0.35)` |
| 边框 | `rgba(255,255,255,0.25-0.4)` |
| 阴影 | `0 8px 32px rgba(14,165,233,0.08-0.12)` |
| 圆角 | `16px / 24px` |

### 配色方案：淡蓝色系

| 角色 | 色值 | 用途 |
|------|------|------|
| 主色 | `#7DD3FC` | 淡蓝主调 |
| 辅色 | `#38BDF8` | 中蓝辅助 |
| 强调色 | `#0EA5E9` | 深蓝 CTA |
| 背景渐变 | `#F0F9FF → #E0F2FE` | 极淡蓝到淡蓝 |
| 文字 | `#0C4A6E` | 深蓝文字 |
| 边框 | `rgba(255,255,255,0.3)` | 玻璃边框 |

### 字体

- 标题：**Outfit**（几何现代风格）
- 正文：**Work Sans**（清晰易读风格）

### UX 规则遵循

- ✅ SVG 图标（非 Emoji）
- ✅ 对比度 ≥ 4.5:1 (WCAG AA)
- ✅ 表单标签可见（非 placeholder-only）
- ✅ 加载状态反馈（骨架屏、spinner）
- ✅ 交互动画 150-300ms
- ✅ `prefers-reduced-motion` 支持
- ✅ 键盘导航与焦点环
- ✅ `aria-label` / `aria-live` 无障碍标签
- ✅ 响应式断点 375/768/1024/1440px
- ✅ 触控目标 ≥ 44px

## 功能模块

### 模块一：用户登录
- 手机号 + 验证码登录（模拟验证码：`123456`）
- 邮箱 + 密码登录
- 密码可见性切换
- 登录后显示剩余免费分析次数

### 模块二：简历上传与解析
- 模拟上传（点击上传区域触发）
- 解析中骨架屏加载动画
- 自动抽取：姓名、学历、毕业时间、专业、技能关键词
- 解析结果可手动编辑修正

### 模块三：岗位智能匹配
- 输入：学历、专业、兴趣方向、期望城市
- 匹配维度：技能匹配(40%) + 学历匹配(30%) + 经验匹配(30%)
- 匹配度环形图可视化
- 颜色标识：≥80%绿色 / 60-79%蓝色 / 40-59%黄色 / <40%灰色
- 每条结果显示匹配理由摘要

### 模块四：岗位详情与收藏
- 点击「查看详情」弹出完整 JD 弹窗
- 收藏到「我的收藏」列表
- 收藏夹可取消收藏、直接进入分析

### 模块五：岗位分析与简历诊断
- 前提：已上传简历 + 已选择心仪岗位
- 分析维度：学历、专业技能、经验、软技能
- 输出报告：
  - 总览匹配度（环形图）
  - ✅ 匹配项清单
  - ❌ 缺失项清单
  - 📝 补充建议（高/中/低优先级）
  - ✏️ 改写示范

### 模块六：收费与额度管理
- 免费权益：每月 3 次免费分析
- 付费方案：
  - 单次 ¥2.9
  - 月度 ¥9.9（推荐）
  - 季度 ¥19.9
- 额度用尽弹出付费引导弹窗
- 模拟支付成功页面

## 用户路径

```
登录 → 上传简历（自动填充）→ 输入兴趣 → 匹配岗位
  → 收藏心仪岗位 → 分析简历 → 查看诊断报告
  → 优化简历 → 额度用尽 → 引导付费
```

## 数据模型

所有数据存储在 `localStorage`，键名前缀 `qie_`：

```javascript
// 用户
qie_currentUser: { id, name, phone/email, freeAnalysisRemaining, subscriptionType }

// 简历
qie_resume_{userId}: { name, education, graduationDate, major, skills[], experienceSummary }

// 收藏列表
qie_favorites_{userId}: [{ id, title, company, city, salary, tags[], favoritedAt }]

// 分析记录
qie_analyses_{userId}: [{ id, jobId, jobTitle, company, matchRate, matchedItems[], missingItems[], suggestions[], rewriteExample, analyzedAt }]

// 匹配表单
qie_matchForm_{userId}: { education, major, interest, city }
```

## 运行方式

### 方式一：直接打开
双击 `index.html` 在浏览器中打开即可。

### 方式二：本地服务器
```bash
# Python
python -m http.server 8000
# 访问 http://localhost:8000

# Node.js
npx serve
```

## 演示账号

由于是纯前端模拟，任意手机号 + 验证码 `123456` 即可登录，或任意邮箱 + 6位以上密码登录。

## API 接口预留

代码中以下部分标注了真实 API 接入位置（当前为模拟实现）：

| 功能 | 模拟位置 | 预留接口 |
|------|----------|----------|
| 发送验证码 | `sendCode()` | `POST /api/sms/send` |
| 登录 | `doLogin()` | `POST /api/auth/login` |
| 简历解析 | `simulateUpload()` | `POST /api/resume/parse` |
| 岗位搜索 | `searchJobs()` | 调用 `mcp-jobs` 或职位聚合 API |
| 简历分析 | `generateAnalysis()` | 调用大语言模型 API |

## 文件结构

```
careergo/
├── index.html    # 完整单页应用
└── README.md     # 本文档
```

## 许可证

MIT
