# GatherGo 开发守则

## 项目概述

- GatherGo是活动发现与发布平台，面向美国市场，未来将全球扩展
- 平台连接用户与活动主办方，提供活动发布、浏览、搜索与参与服务
- MVP阶段专注核心功能，保证快速上线与验证

## 技术栈规范

### 前端技术

- **必须使用** React（v18+）开发，结合现代React模式和最佳实践
- **必须使用** Tailwind CSS进行样式开发，遵循响应式设计原则
- **禁止使用** jQuery或其他与React生态冲突的库
- **必须实现** PWA特性，支持移动设备访问体验

### 后端技术

- **必须使用** Node.js（Express/NestJS）构建API服务
- **必须使用** PostgreSQL作为主数据库
- **必须使用** Redis处理缓存与会话
- **必须选用** Algolia或Elasticsearch实现搜索功能

### 认证与安全

- **必须集成** Firebase Auth或Auth0处理用户认证
- **必须实现** CCPA隐私合规要求
- **必须使用** HTTPS，JWT令牌管理API访问
- **禁止在前端** 存储敏感信息

## 项目结构指南

### 目录结构

```
GatherGo/
├── frontend/                # React前端应用
│   ├── public/              # 静态资源文件
│   │   ├── index.html       # HTML入口文件
│   │   ├── favicon.ico      # 网站图标
│   │   └── assets/          # 静态资源（图片、字体等）
│   ├── src/                 # 源代码
│   │   ├── components/      # 共享UI组件
│   │   │   ├── layout/      # 布局组件
│   │   │   ├── common/      # 通用UI组件
│   │   │   ├── events/      # 活动相关组件
│   │   │   └── user/        # 用户相关组件
│   │   ├── pages/           # 页面组件
│   │   ├── hooks/           # 自定义React Hooks
│   │   ├── context/         # React Context
│   │   ├── utils/           # 工具函数
│   │   ├── services/        # API服务封装
│   │   ├── types/           # TypeScript类型定义
│   │   ├── styles/          # 全局样式
│   │   ├── App.tsx          # 应用根组件
│   │   └── index.tsx        # 应用入口点
│   ├── tests/               # 测试文件
│   ├── .env                 # 环境变量
│   ├── package.json         # 依赖管理
│   ├── tsconfig.json        # TypeScript配置
│   └── README.md            # 前端文档
├── backend/                 # 后端API服务
│   ├── src/                 # 源代码
│   │   ├── controllers/     # 请求处理器
│   │   ├── models/          # 数据模型
│   │   ├── services/        # 业务逻辑
│   │   ├── routes/          # API路由
│   │   ├── utils/           # 工具函数
│   │   ├── middleware/      # 中间件
│   │   ├── config/          # 配置文件
│   │   └── index.js         # 应用入口点
│   ├── tests/               # 测试文件
│   ├── .env                 # 环境变量
│   ├── package.json         # 依赖管理
│   └── README.md            # 后端文档
├── shared/                  # 前后端共享代码
│   ├── constants/           # 共享常量
│   └── types/               # 共享类型定义
├── docs/                    # 项目文档
├── scripts/                 # 部署脚本和工具
└── README.md                # 项目总体说明
```

### 关键文件交互规范

- 修改`backend/src/models/`目录下的数据模型时，**必须同步更新**：
  - `shared/types/`中的相应类型定义
  - `frontend/src/services/`中的相应API调用方法
- 修改`backend/src/routes/`目录下的API路由时，**必须同步更新**：
  - API文档
  - 前端的服务调用代码

## 命名与代码规范

### 文件命名

- React组件文件：**必须使用** PascalCase (例：`EventCard.tsx`)
- API路由文件：**必须使用** kebab-case (例：`event-routes.js`)
- 工具函数文件：**必须使用** camelCase (例：`dateUtils.js`)

### API路径命名

- API路径**必须使用**RESTful风格
- 必须遵循格式：`/api/[资源]/[操作]`
- 例如：
  - ✅ `/api/events` - 获取活动列表
  - ✅ `/api/events/:id` - 获取特定活动
  - ❌ `/api/getEvent` - 非RESTful风格

### 数据库表命名

- 表名**必须使用**蛇形命名法(snake_case)
- 表名**必须使用**复数形式
- 例如：
  - ✅ `events`, `users`, `event_tags`
  - ❌ `Event`, `User`, `eventTag`

### 组件规范

- 组件**必须采用**功能分区，并遵循单一职责原则
- UI与业务逻辑**必须分离**
- 组件接口(Props)**必须有**TypeScript类型定义

## 核心功能实现指南

### 活动发布流程

- **必须实现**多步骤表单提交流程
- **必须在客户端**进行表单验证
- **必须在服务端**进行二次验证
- **必须支持**图片上传功能，使用AWS S3或类似服务
- **审核流程必须**先自动审核(敏感词过滤)再人工审核

### 搜索与筛选系统

- **必须支持**关键词搜索和多维筛选
- **必须实现**地理位置搜索功能
- **必须使用**Algolia/Elasticsearch实现复杂搜索
- **必须实现**搜索高亮与自动补全功能

### 用户认证与授权

- **必须支持**邮箱注册和社交账号登录
- **必须实现**角色权限系统，区分普通用户/主办方/管理员
- **必须处理**令牌过期与刷新逻辑

### 地图集成

- **必须使用**Google Maps或Mapbox展示活动地点
- **必须支持**地点搜索与导航功能
- **必须处理**地理编码与反向地理编码功能

## 任务层级结构规范

### Epic（史诗）

- **定义**：大型自包含功能模块，如"活动发现系统"
- **范围**：一次只有一个活跃的Epic，其下包含多个Story
- **命名规范**：**必须**清晰表达主要功能领域，使用"系统"、"平台"等后缀
- **描述要求**：**必须**简洁说明目标和价值，不超过100字
- **示例**：
  - ✅ "活动发现系统" - 实现用户浏览和搜索活动的核心功能
  - ❌ "实现活动功能" - 描述过于模糊

### Story（故事）

- **定义**：可实施的功能单元，如"首页活动推荐模块"
- **范围**：**必须**属于一个Epic，包含多个Task
- **命名规范**：**必须**使用"模块"、"功能"等后缀，避免技术术语
- **描述要求**：**必须**说明功能需求和用户价值，不超过200字
- **示例**：
  - ✅ "首页活动推荐模块" - 实现首页活动推荐功能
  - ❌ "React组件开发" - 使用了技术术语而非功能描述

### Task（任务）

- **定义**：技术实现步骤，如"轮播图组件开发"
- **范围**：**必须**属于一个Story，可能包含Subtask
- **命名规范**：**必须**使用动词开头，清晰说明技术实现内容
- **描述要求**：**必须**包含详细技术实现内容，可包含技术要点
- **示例**：
  - ✅ "轮播图组件开发" - 开发首页轮播图组件
  - ❌ "首页轮播" - 缺少动词和技术实现内容

### Subtask（子任务）

- **定义**：细粒度工作项，如"轮播图图片加载优化"
- **范围**：**必须**属于一个Task
- **命名规范**：**必须**使用具体动作描述，高度专注
- **描述要求**：**必须**包含具体技术细节和验证标准
- **示例**：
  - ✅ "轮播图图片加载优化" - 优化轮播图图片加载速度和性能
  - ❌ "图片优化" - 描述过于模糊

### 依赖关系管理

- **横向依赖**：同级任务间的依赖**必须**使用ID引用
- **纵向依赖**：子任务默认依赖父任务，**无需**显式声明
- **跨级依赖**：**必须避免**跨越层级的依赖关系
- **循环依赖**：**严禁**创建循环依赖

## 任务实施流程规范

### 初始化阶段

- **验证目录存在**：**必须**确认相关目录已创建
- **定位架构文档**：**必须**查阅相关架构和设计文档
- **任务状态标记**：**必须**将任务标记为进行中
- **依赖项检查**：**必须**确认所有依赖任务已完成

### 开发流程

- **测试驱动开发**：**必须**先编写测试，再实现功能
- **状态定期更新**：**必须**每完成一个主要步骤更新状态
- **实施记录**：**必须**记录重要决策和使用的命令
- **代码规范遵循**：**必须**确保符合项目代码规范

### 完成要求

- **测试通过**：**必须**所有测试用例通过
- **文档更新**：**必须**更新相关文档
- **用户确认**：**必须**获得用户批准
- **代码审查**：**必须**通过代码审查

### 验证标准

- **功能验证**：**必须**符合任务验证标准
- **性能要求**：**必须**符合性能指标
- **兼容性测试**：**必须**通过兼容性测试
- **安全检查**：**必须**通过安全审核

## AI决策优先级指南

### 技术选择优先级

1. 安全性
2. 性能
3. 代码可维护性
4. 开发速度

### 功能实现优先级

1. MVP核心功能（活动浏览、搜索、发布、审核）
2. 移动端适配
3. 数据分析与报表
4. 高级互动功能

### 错误处理优先级

1. 用户数据安全相关错误
2. 核心功能错误（活动浏览/发布/搜索）
3. 用户体验错误（UI/UX问题）
4. 非关键功能错误

### 任务处理优先级

1. Epic层级任务（架构基础）
2. Story层级任务（功能模块）
3. Task层级任务（具体实现）
4. Subtask层级任务（优化改进）

### 模糊情况决策指南

- 当功能实现方式不明确时，**优先参考**现有类似功能的实现模式
- 当新增字段/功能时，**必须优先考虑**是否会影响已有数据结构
- 当UI设计不明确时，**必须遵循**移动优先原则设计界面
- 当任务依赖关系不明确时，**必须遵循**层级结构规范解决

## 禁止事项

- **严禁**将敏感配置（API密钥、数据库凭证）硬编码在源代码中
- **严禁**在前端存储用户敏感信息
- **严禁**绕过审核机制直接发布活动
- **严禁**混用不同的UI风格与组件库
- **严禁**忽略数据验证与安全检查
- **严禁**使用deprecated API或不受支持的库
- **严禁**在核心功能路径上引入复杂的实验性功能
- **严禁**创建跨越多个层级的任务依赖
- **严禁**忽略任务初始化和完成要求

## 命令执行规范

### MCP服务使用

- **必须使用** desktop-commander MCP服务执行系统命令
- **禁止使用** 直接的命令行调用或非安全的命令执行方式
- **必须检查** 命令执行的结果和错误信息
- **必须记录** 关键命令的执行日志

### 命令执行安全

- **严禁执行** 未经验证的用户输入作为命令
- **必须限制** 命令执行的权限范围
- **必须使用** 参数化的命令调用方式
- **必须处理** 命令执行过程中的异常情况

### 文件操作规范

- **必须使用** desktop-commander的文件操作功能进行文件读写
- **必须验证** 文件路径的安全性和有效性
- **必须处理** 文件操作过程中的错误和异常
- **必须遵循** 最小权限原则访问文件系统

## 实施示例

### ✅ 正确的活动卡片组件实现

```tsx
// components/events/EventCard.tsx
import { formatDate } from 'utils/dateUtils';
import { LazyLoadImage } from 'react-lazy-load-image-component';

type EventCardProps = {
  id: string;
  title: string;
  dateTime: string;
  location: string;
  imageUrl: string;
  tags: string[];
}

export const EventCard = ({ id, title, dateTime, location, imageUrl, tags }: EventCardProps) => {
  return (
    <a href={`/events/${id}`} className="group">
      <div className="rounded-lg overflow-hidden shadow-md hover:shadow-lg transition-shadow">
        <div className="relative h-48">
          <LazyLoadImage
            src={imageUrl || '/placeholder.jpg'} 
            alt={title}
            className="object-cover w-full h-full"
            effect="blur"
          />
        </div>
        <div className="p-4">
          <h3 className="text-lg font-semibold">{title}</h3>
          <p className="text-sm text-gray-600">{formatDate(dateTime)}</p>
          <p className="text-sm text-gray-600">{location}</p>
          <div className="mt-2 flex flex-wrap gap-1">
            {tags.slice(0, 3).map(tag => (
              <span key={tag} className="text-xs bg-gray-100 px-2 py-1 rounded">
                {tag}
              </span>
            ))}
          </div>
        </div>
      </div>
    </a>
  );
};
```

### ✅ 正确的MCP命令执行示例

```typescript
// utils/commandUtils.ts
import { mcp_desktop_commander_execute_command } from 'mcp-services';

export const executeCommand = async (command: string): Promise<string> => {
  try {
    const result = await mcp_desktop_commander_execute_command({
      command,
      timeout_ms: 30000
    });
    
    if (result.error) {
      console.error(`Command execution error: ${result.error}`);
      throw new Error(result.error);
    }
    
    return result.output;
  } catch (error) {
    console.error('Failed to execute command:', error);
    throw error;
  }
};

// 使用示例
const installDependencies = async () => {
  try {
    const output = await executeCommand('npm install --save react-lazy-load-image-component');
    console.log('Installation successful:', output);
    return true;
  } catch (error) {
    console.error('Installation failed:', error);
    return false;
  }
};
```

### ❌ 错误的命令执行示例

```javascript
// 错误示例：不安全的命令执行方式
const runCommand = (cmd) => {
  const { exec } = require('child_process');
  return new Promise((resolve, reject) => {
    exec(cmd, (error, stdout, stderr) => {
      if (error) {
        reject(error);
        return;
      }
      resolve(stdout);
    });
  });
};

// 危险：直接拼接用户输入作为命令
const installPackage = async (packageName) => {
  const command = `npm install ${packageName}`;  // 未验证的用户输入
  return await runCommand(command);
};
``` 