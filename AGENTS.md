# AGENTS.md

## 项目概览

AI 提示词引导生成器 - 通过分步问答引导用户生成高质量 AI 提示词的 Web 应用。支持生文、生图、生视频、生PPT 四种类型。

## 技术栈

- **Framework**: Next.js 16 (App Router)
- **Core**: React 19
- **Language**: TypeScript 5
- **UI**: shadcn/ui + Tailwind CSS 4
- **Icons**: lucide-react

## 目录结构

```
src/
├── app/
│   ├── page.tsx                    # 首页 - 四种类型选择卡片
│   ├── guide/page.tsx              # 引导页 - 分步问答流程
│   ├── result/page.tsx             # 结果页 - 展示生成的提示词
│   ├── api/analyze-image/route.ts  # 图片分析 API
│   ├── layout.tsx                  # 根布局
│   └── globals.css                 # 全局样式 + 动画
├── components/
│   ├── prompt-wizard.tsx           # 核心向导组件
│   ├── image-uploader.tsx          # 图片上传组件
│   └── ui/                         # shadcn/ui 组件
└── lib/
    └── prompt-data.ts              # 提示词数据定义与生成逻辑
```

## 核心功能

1. **首页**: 四张卡片选择生成类型（生文/生图/生视频/生PPT）
2. **引导流程**: 分步问答，每步一个问题+选项，有进度条
3. **参考图上传**: 支持拖拽上传1-3张图片，AI分析视觉特征
4. **结果页**: 展示生成的提示词，支持一键复制

## 关键文件

- `src/lib/prompt-data.ts`: 四种类型的引导步骤定义和提示词生成逻辑
- `src/components/prompt-wizard.tsx`: 向导核心组件，处理步骤切换和状态管理
- `src/components/image-uploader.tsx`: 图片上传与分析组件

## 开发命令

- `pnpm dev` - 启动开发服务器
- `pnpm build` - 构建生产版本
- `pnpm ts-check` - TypeScript 类型检查
- `pnpm lint` - ESLint 检查

## 设计规范

详见 `DESIGN.md` - 暖灰底色 + 四种类型各有专属色彩标识（琥珀/紫罗兰/天蓝/翡翠绿）
