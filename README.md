# 汉字学习与管理系统

## 项目简介
本系统基于Django框架开发，专注于汉字数据的存储、管理与展示。支持汉字特征记录、图片管理、简繁字体识别、数据导出等功能。

## 功能特性

### 核心功能
| 模块          | 功能描述                                                                 |
|---------------|--------------------------------------------------------------------------|
| 汉字特征管理  | 支持编号、字符、拼音、笔画数、结构类型等12个字段；7种结构分类；双图片上传 |
| 图片处理      | 自动重命名、路径规范化、存在性校验                                       |
| OCR识别       | 简繁双引擎识别，可信度比较算法，图像预处理                               |

### 扩展功能
| 模块          | 功能描述                                                                 |
|---------------|--------------------------------------------------------------------------|
| 数据导出      | ZIP打包下载、Excel报表生成                                               |
| 管理系统      | Django Admin定制，多字段搜索过滤，笔画数优先排序                         |

## 技术栈
| 类别        | 技术/工具                 | 版本      |
|-----------|-----------------------|---------|
| 后端框架    | Django                | 4.2     |
| 前端框架    | Bootstrap             | 5.3     |
| 数据库      | SQLite3               | 3.37    |
| OCR引擎    | EasyOCR               | 1.7.0   |
| 图像处理    | Pillow                | 9.5     |
| 部署       | ASGI                  | 3.0     |

## 安装与部署

### 开发环境
```bash
# 克隆仓库
git clone [仓库地址]
cd d:\hanziproject-副本

# 安装依赖
pip install -r requirements.txt

# 数据库迁移
python manage.py makemigrations
python manage.py migrate

# 静态文件收集
python manage.py collectstatic

# 运行开发服务器
python manage.py runserver 0.0.0.0:8000
```

### 生产环境建议
1. 在`hanzi_project/settings.py`中：
   ```python
   DEBUG = False
   ALLOWED_HOSTS = ['your-domain.com']
   SECRET_KEY = 'your-secret-key'
   ```
2. 使用Nginx + uWSGI部署
3. 定期备份`db.sqlite3`文件

## 使用说明

### 后台管理
1. 访问 `/admin` 使用管理员账号登录
2. 支持功能：
   - 批量编辑汉字特征
   - 图片路径校验
   - 数据导出（Excel/ZIP）

### 前端操作
1. **添加汉字**：
   - 上传书写图片和标准图片
   - 自动生成汉字ID（结构类型+序号）

2. **编辑功能**：
   - 结构类型变更触发文件重命名
   - 事务处理保证数据一致性

3. **识别功能示例**：
   ```python
   from hanzi_app.recognition import recognize_hanzi

   result, font_type = recognize_hanzi("path/to/image.jpg")
   ```

## 目录结构
```
d:\hanziproject-副本
├── hanzi_app/               # 核心应用
│   ├── admin.py            # 后台管理配置
│   ├── models.py           # 数据模型定义（Hanzi类）
│   ├── recognition.py      # OCR识别模块
│   ├── urls.py             # 应用路由配置
│   └── views.py            # 业务逻辑处理（70%代码量）
├── hanzi_project/          # 项目配置
│   ├── settings.py         # 项目设置
│   └── urls.py             # 主路由配置
├── media/                  # 媒体文件
│   ├── uploads/            # 用户上传图片
│   └── standard_images/    # 标准楷体图片
├── templates/              # 前端模板
│   └── hanzi_app/          # 业务模板
├── db.sqlite3              # 数据库文件
└── requirements.txt        # 依赖列表
```

## API文档

### 汉字详情接口
- **端点**：`/hanzi/<str:hanzi_id>/`
- **方法**：GET
- **返回**：HTML页面（`templates/hanzi_app/detail.html`）

### 数据下载接口
- **端点**：`/download/<str:filename>/`
- **方法**：GET
- **响应**：
  - 成功：ZIP文件流
  - 失败：JSON错误信息

## 贡献指南
1. 问题报告：提交GitHub Issue
2. 功能建议：通过Pull Request提交
3. 代码规范：
   - Django最佳实践
   - PEP8 Python规范
   - 重要函数必须包含docstring

## 许可证
MIT License（详见项目根目录LICENSE文件）


**优化说明**：
1. 采用表格形式增强数据展示
2. 统一代码块格式，增加语法高亮
3. 突出关键配置项和示例代码
4. 优化目录结构显示
5. 调整标题层级，增强文档可读性
6. 补充技术栈版本信息
7. 修复部分路径格式问题
