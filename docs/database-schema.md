# GatherGo 数据库架构设计

## 数据库选型

- **主数据库**: PostgreSQL 14+
- **缓存数据库**: Redis 6+
- **搜索引擎**: Algolia

## 表结构设计

### users 表 (用户)

| 字段名 | 类型 | 说明 | 约束 |
|--------|------|------|------|
| id | UUID | 用户唯一标识 | PRIMARY KEY |
| email | VARCHAR(255) | 用户邮箱 | UNIQUE, NOT NULL |
| username | VARCHAR(50) | 用户名 | UNIQUE, NOT NULL |
| password_hash | VARCHAR(255) | 密码哈希值 | NOT NULL |
| first_name | VARCHAR(50) | 名 | |
| last_name | VARCHAR(50) | 姓 | |
| avatar_url | VARCHAR(255) | 头像URL | |
| bio | TEXT | 个人简介 | |
| location | VARCHAR(100) | 所在地区 | |
| role | VARCHAR(20) | 用户角色 | DEFAULT 'user' |
| created_at | TIMESTAMP | 创建时间 | DEFAULT NOW() |
| updated_at | TIMESTAMP | 更新时间 | DEFAULT NOW() |
| last_login | TIMESTAMP | 最后登录时间 | |
| is_verified | BOOLEAN | 是否已验证邮箱 | DEFAULT FALSE |
| is_active | BOOLEAN | 账户是否活跃 | DEFAULT TRUE |

### events 表 (活动)

| 字段名 | 类型 | 说明 | 约束 |
|--------|------|------|------|
| id | UUID | 活动唯一标识 | PRIMARY KEY |
| title | VARCHAR(100) | 活动标题 | NOT NULL |
| description | TEXT | 活动详细描述 | NOT NULL |
| short_description | VARCHAR(255) | 活动简短描述 | |
| organizer_id | UUID | 主办方用户ID | FOREIGN KEY, NOT NULL |
| start_time | TIMESTAMP | 开始时间 | NOT NULL |
| end_time | TIMESTAMP | 结束时间 | NOT NULL |
| timezone | VARCHAR(50) | 时区 | DEFAULT 'UTC' |
| location_name | VARCHAR(255) | 地点名称 | |
| address | VARCHAR(255) | 详细地址 | |
| city | VARCHAR(100) | 城市 | NOT NULL |
| state | VARCHAR(100) | 州/省 | NOT NULL |
| country | VARCHAR(100) | 国家 | DEFAULT 'United States' |
| latitude | DECIMAL(10,8) | 纬度 | |
| longitude | DECIMAL(11,8) | 经度 | |
| is_online | BOOLEAN | 是否为线上活动 | DEFAULT FALSE |
| online_url | VARCHAR(255) | 线上活动链接 | |
| cover_image_url | VARCHAR(255) | 封面图片URL | |
| capacity | INTEGER | 最大容量 | |
| price | DECIMAL(10,2) | 价格 | DEFAULT 0 |
| is_free | BOOLEAN | 是否免费 | DEFAULT TRUE |
| currency | VARCHAR(3) | 货币类型 | DEFAULT 'USD' |
| status | VARCHAR(20) | 活动状态 | DEFAULT 'draft' |
| visibility | VARCHAR(20) | 可见性 | DEFAULT 'public' |
| created_at | TIMESTAMP | 创建时间 | DEFAULT NOW() |
| updated_at | TIMESTAMP | 更新时间 | DEFAULT NOW() |
| published_at | TIMESTAMP | 发布时间 | |
| is_featured | BOOLEAN | 是否推荐 | DEFAULT FALSE |
| is_approved | BOOLEAN | 是否通过审核 | DEFAULT FALSE |
| views_count | INTEGER | 浏览次数 | DEFAULT 0 |
| likes_count | INTEGER | 点赞次数 | DEFAULT 0 |

### event_categories 表 (活动类别)

| 字段名 | 类型 | 说明 | 约束 |
|--------|------|------|------|
| id | UUID | 类别唯一标识 | PRIMARY KEY |
| name | VARCHAR(50) | 类别名称 | UNIQUE, NOT NULL |
| description | VARCHAR(255) | 类别描述 | |
| icon | VARCHAR(100) | 类别图标 | |
| color | VARCHAR(7) | 类别颜色 | |
| created_at | TIMESTAMP | 创建时间 | DEFAULT NOW() |
| updated_at | TIMESTAMP | 更新时间 | DEFAULT NOW() |

### event_category_mappings 表 (活动-类别映射)

| 字段名 | 类型 | 说明 | 约束 |
|--------|------|------|------|
| event_id | UUID | 活动ID | FOREIGN KEY, NOT NULL |
| category_id | UUID | 类别ID | FOREIGN KEY, NOT NULL |
| created_at | TIMESTAMP | 创建时间 | DEFAULT NOW() |

_PRIMARY KEY (event_id, category_id)_

### event_tags 表 (活动标签)

| 字段名 | 类型 | 说明 | 约束 |
|--------|------|------|------|
| id | UUID | 标签唯一标识 | PRIMARY KEY |
| name | VARCHAR(50) | 标签名称 | UNIQUE, NOT NULL |
| created_at | TIMESTAMP | 创建时间 | DEFAULT NOW() |

### event_tag_mappings 表 (活动-标签映射)

| 字段名 | 类型 | 说明 | 约束 |
|--------|------|------|------|
| event_id | UUID | 活动ID | FOREIGN KEY, NOT NULL |
| tag_id | UUID | 标签ID | FOREIGN KEY, NOT NULL |
| created_at | TIMESTAMP | 创建时间 | DEFAULT NOW() |

_PRIMARY KEY (event_id, tag_id)_

### event_images 表 (活动图片)

| 字段名 | 类型 | 说明 | 约束 |
|--------|------|------|------|
| id | UUID | 图片唯一标识 | PRIMARY KEY |
| event_id | UUID | 活动ID | FOREIGN KEY, NOT NULL |
| url | VARCHAR(255) | 图片URL | NOT NULL |
| alt_text | VARCHAR(255) | 替代文本 | |
| display_order | INTEGER | 显示顺序 | DEFAULT 0 |
| created_at | TIMESTAMP | 创建时间 | DEFAULT NOW() |

### registrations 表 (活动报名)

| 字段名 | 类型 | 说明 | 约束 |
|--------|------|------|------|
| id | UUID | 报名唯一标识 | PRIMARY KEY |
| event_id | UUID | 活动ID | FOREIGN KEY, NOT NULL |
| user_id | UUID | 用户ID | FOREIGN KEY, NOT NULL |
| status | VARCHAR(20) | 报名状态 | DEFAULT 'confirmed' |
| registration_time | TIMESTAMP | 报名时间 | DEFAULT NOW() |
| check_in_time | TIMESTAMP | 签到时间 | |
| ticket_type | VARCHAR(50) | 票种类型 | |
| ticket_price | DECIMAL(10,2) | 票价 | |
| quantity | INTEGER | 数量 | DEFAULT 1 |
| notes | TEXT | 备注 | |

## 索引设计

### users 表索引
- `email_idx`: 邮箱索引
- `username_idx`: 用户名索引
- `role_idx`: 角色索引

### events 表索引
- `organizer_id_idx`: 主办方ID索引
- `start_time_idx`: 开始时间索引
- `city_state_idx`: 城市和州复合索引
- `status_idx`: 状态索引
- `is_featured_idx`: 推荐标记索引
- `is_approved_idx`: 审核标记索引
- `location_idx`: 地理位置索引 (经纬度)

### registrations 表索引
- `event_id_idx`: 活动ID索引
- `user_id_idx`: 用户ID索引
- `status_idx`: 状态索引

## 数据关系图

```
users 1 --< events N (一个用户可以创建多个活动)
events N >-- 1 users (一个活动由一个用户创建)

events N --< event_images N (一个活动可以有多张图片)
events N --< event_category_mappings N (一个活动可以属于多个类别)
events N --< event_tag_mappings N (一个活动可以有多个标签)
events N --< registrations N (一个活动可以有多个报名)

users N >-- registrations N (一个用户可以报名多个活动)
```

## 扩展考虑

1. **分区策略**: 考虑按地理区域或时间对大表进行分区
2. **缓存设计**: 活动列表和热门活动适合使用Redis缓存
3. **搜索优化**: 使用Algolia维护活动索引，支持复杂搜索
4. **审计日志**: 考虑添加audit_logs表追踪关键操作 