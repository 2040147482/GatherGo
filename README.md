# GatherGo 🎯

> 本地活动发现平台 - 基于位置的智能活动推荐与社交互动应用

## 项目概述

GatherGo是一个创新的本地活动发现平台，旨在连接用户与周边精彩活动。通过智能推荐算法和位置服务，帮助用户发现感兴趣的本地活动，促进社区互动和社交连接。

## 核心功能

- 🔍 **智能活动推荐**：基于用户偏好和位置的个性化推荐
- 📍 **位置服务**：精准的地理位置匹配和距离计算
- 👥 **社交互动**：用户评论、评分和社交分享
- 📱 **移动优先**：响应式设计，完美适配移动设备
- 🔐 **安全认证**：完整的用户认证和授权系统

## 技术架构

### 前端
- **Framework**: Next.js 14 (App Router)
- **UI Library**: Tailwind CSS + Shadcn/ui
- **State Management**: Zustand
- **HTTP Client**: Axios
- **Maps**: 高德地图 API

### 后端
- **Framework**: NestJS
- **Database**: PostgreSQL + Redis
- **Authentication**: JWT + Passport
- **File Storage**: AWS S3
- **Email Service**: AWS SES

### 部署
- **Frontend**: Vercel
- **Backend**: AWS ECS
- **Database**: AWS RDS (PostgreSQL) + ElastiCache (Redis)
- **CDN**: AWS CloudFront

## 项目结构

```
GatherGo/
├── frontend/          # Next.js 前端应用
├── backend/           # NestJS 后端API
├── docs/              # 项目文档
├── scripts/           # 构建和部署脚本
└── .github/           # GitHub Actions CI/CD
```

## 开发环境设置

### 前端 (Next.js)
```bash
cd frontend
npm install
npm run dev
```

### 后端 (NestJS)
```bash
cd backend
npm install
npm run start:dev
```

## 贡献指南

1. Fork 项目
2. 创建功能分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

## 许可证

本项目采用 MIT 许可证 - 查看 [LICENSE](LICENSE) 文件了解详情

## 联系我们

- 项目链接: [https://github.com/YOUR_USERNAME/GatherGo](https://github.com/YOUR_USERNAME/GatherGo)
- 问题反馈: [Issues](https://github.com/YOUR_USERNAME/GatherGo/issues)

---
Made with ❤️ by GatherGo Team