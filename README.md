# Awesun UI Locator - 截图 UI 元素定位器

一个用于分析桌面截图并精确定位UI元素的AI技能。通过AI视觉模型识别截图中的按钮、输入框、图标等界面元素，并返回标准化坐标位置。

## 🚀 核心功能

- **智能识别**：自动识别截图中的各种UI元素（按钮、输入框、图标、文本等）
- **精确定位**：返回元素的标准化坐标 (x_norm, y_norm)，范围 [0.0, 1.0]
- **多种元素支持**：支持按钮、输入框、图标、导航元素、文本等常见UI组件
- **多格式支持**：兼容PNG、JPEG、JPG等常见图片格式
- **上下文理解**：根据用户的自然语言描述准确匹配目标元素


## 🎯 使用场景

- **自动化测试**：为自动化脚本提供UI元素坐标
- **用户体验分析**：分析界面布局和元素位置
- **辅助工具开发**：为残障用户开发辅助工具
- **界面逆向工程**：分析和理解第三方应用界面
- **脚本录制重放**：记录用户操作并自动回放

## 📋 工作流程

### 1. 读取截图
```bash
# 提供截图文件路径
/path/to/screenshot.png
```

### 2. 描述目标元素
```text
用户：找到登录按钮的位置
用户：右上角的设置图标在哪里
用户：位于页面底部的提交按钮
```

### 3. 获取坐标结果
```json
{
  "found": true,
  "element": "登录按钮",
  "coordinates": {
    "x": 0.5,
    "y": 0.417
  },
  "confidence": "high",
  "description": "位于页面中央偏上的蓝色按钮，显示'登录'文字"
}
```

## 🔧 安装指南

### 前置条件

1. **向日葵客户端** - 用于远程控制功能
   - 版本要求：16.3.2 或更高
   - 下载地址：[https://sunlogin.oray.com](https://sunlogin.oray.com)

2. **支持的AI编辑器**：
   - Claude Code
   - Open Code  
   - 🦞OpenClaw

### 📦 自动安装

我们提供了针对不同AI编辑器的一键安装脚本：

#### Claude Code 安装

```bash
# 下载并执行安装脚本
curl -sSL https://github.com/OrayDev/awesun-skill/raw/main/scripts/install-claude-code.sh | bash

# 或者手动下载执行
wget https://github.com/OrayDev/awesun-skill/raw/main/scripts/install-claude-code.sh
chmod +x install-claude-code.sh
./install-claude-code.sh
```

**Windows 用户**：
```powershell
# PowerShell 执行
iwr -useb https://github.com/OrayDev/awesun-skill/raw/main/scripts/install-claude-code.ps1 | iex
```

#### Open Code 安装

```bash
# Linux/macOS 用户
curl -sSL https://github.com/OrayDev/awesun-skill/raw/main/scripts/install-opencode.sh | bash

# 或者
wget https://github.com/OrayDev/awesun-skill/raw/main/scripts/install-opencode.sh
chmod +x install-opencode.sh
./install-opencode.sh
```

**Windows 用户**：
```powershell
# PowerShell 执行
iwr -useb https://github.com/OrayDev/awesun-skill/raw/main/scripts/install-opencode.ps1 | iex
```

#### 🦞OpenClaw 安装

```bash
# Linux/macOS 用户
curl -sSL https://github.com/OrayDev/awesun-skill/raw/main/scripts/install-openclaw.sh | bash

# 或者
wget https://github.com/OrayDev/awesun-skill/raw/main/scripts/install-openclaw.sh
chmod +x install-openclaw.sh
./install-openclaw.sh
```

### 🔨 手动安装

如果自动安装失败，可以按以下步骤手动安装：

1. **克隆仓库**：
```bash
git clone https://github.com/OrayDev/awesun-ui-locator.git
cd awesun-ui-locator
```

2. **复制技能文件**：
```bash
# 找到你的AI编辑器配置目录
# Claude Code: ~/.claude-code/skills/
# Open Code: ~/.opencode/skills/  
# OpenClaw: ~/.openclaw/skills/

# 复制技能文件
cp -r . ~/.claude-code/skills/awesun-ui-locator/
```

3. **重启AI编辑器**

### ✅ 安装验证

安装完成后，在AI编辑器中测试：

```text
请帮我分析这张截图，找到登录按钮的位置
[提供一张包含登录按钮的截图]
```

如果AI能够识别并返回坐标信息，说明安装成功。

## 📋 技能规格

### 支持的UI元素类型

| 元素类型 | 描述 | 示例 |
|---------|------|------|
| **按钮** | 各种类型的操作按钮 | 登录、提交、取消、确认 |
| **输入框** | 文本输入区域 | 搜索框、用户名、密码框 |
| **图标** | 功能性图标元素 | 设置齿轮、汉堡菜单、关闭按钮 |
| **导航** | 导航相关元素 | 标签页、分页器、面包屑 |
| **文本** | 文字内容元素 | 标题、链接、标签 |

### 坐标系统

- **原点**：左上角 (0.0, 0.0)
- **范围**：X轴和Y轴均为 [0.0, 1.0]
- **精度**：小数点后6位
- **返回**：元素中心点的归一化坐标

### 查找策略

1. **位置描述**：支持相对位置描述（"左上角"、"页面中央"、"右下角"）
2. **颜色特征**：结合颜色信息提高识别准确度（"蓝色按钮"、"红色图标"）
3. **文字内容**：基于显示文字精确匹配（"显示'确认'的按钮"）
4. **上下文关系**：考虑元素间的层级关系（"弹窗中的关闭按钮"）

## 🎯 使用示例

### 示例1：定位登录按钮

**输入**：
- 图片路径：`/Users/demo/desktop-screenshot.png`
- 用户描述：`"找到登录按钮"`

**输出**：
```json
{
  "found": true,
  "element": "登录按钮",
  "coordinates": {
    "x": 0.5,
    "y": 0.417
  },
  "confidence": "high",
  "description": "位于页面中央偏上的蓝色按钮，显示'登录'文字"
}
```

### 示例2：定位菜单图标

**输入**：
- 图片路径：`/Users/demo/app-interface.png`
- 用户描述：`"右上角的汉堡菜单图标"`

**输出**：
```json
{
  "found": true,
  "element": "菜单图标",
  "coordinates": {
    "x": 0.938,
    "y": 0.067
  },
  "confidence": "high",
  "description": "位于右上角的汉堡菜单图标（三条横线）"
}
```

### 示例3：未找到元素

**输出**：
```json
{
  "found": false,
  "element": "搜索按钮",
  "reason": "未能在图片中找到匹配的元素",
  "suggestions": [
    "可能是滚动区域外的内容",
    "元素可能被其他内容遮挡",
    "描述可能不够精确，尝试更详细的描述"
  ]
}
```

## 📚 参考资料

- **技能详细说明**：[SKILL.md](SKILL.md)
- **UI元素识别指南**：[references/ui_patterns.md](references/ui_patterns.md)
- **坐标计算工具**：[scripts/coordinate_utils.py](scripts/coordinate_utils.py)

## 🤝 贡献指南

我们欢迎社区贡献！如果你有改进建议或发现了bug：

1. Fork 此仓库
2. 创建功能分支：`git checkout -b feature/your-feature`
3. 提交修改：`git commit -m "Add some feature"`
4. 推送分支：`git push origin feature/your-feature`
5. 创建 Pull Request

## ⚠️ 注意事项

- 确保提供的截图清晰且包含目标元素
- 使用尽可能具体的描述来提高识别准确度
- 大文件处理可能需要更多时间
- 某些复杂界面可能需要多次尝试不同的描述方式

## 📄 许可证

本项目采用 [MIT License](LICENSE) 许可证。

## 📞 支持与反馈

如果遇到问题或需要帮助：

- 提交 [Issue](https://github.com/OrayDev/awesun-ui-locator/issues)
- 联系邮箱：support@oray.com
- 访问：[向日葵官网](https://sunlogin.oray.com)

---

**Made with ❤️ by Oray Team**