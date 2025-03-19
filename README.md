
```markdown
# 汉字学习与管理系统（hanziproject-副本）

## 项目简介
本项目是一个基于Django框架开发的汉字学习与管理系统，主要用于汉字数据的存储、管理和展示。系统支持汉字特征记录、图片管理、简繁字体识别、数据导出等功能，适用于汉字教学研究和文化传承机构。

## 功能特性
### 核心功能
- **汉字特征管理**
  - 完整字段：编号、汉字字符、拼音、笔画数、结构类型、简繁体、等级等
  - 支持图片上传（用户书写图片和标准楷体图片）
  - 结构类型分类：7种结构（左右/上下/包围等）
  
- **图片处理**
  - 自动文件重命名（<mcsymbol name="edit_hanzi" filename="views.py" path="d:\hanziproject-副本\hanzi_app\views.py" startline="250" type="function"></mcsymbol>）
  - 图片路径规范化处理
  - 文件存在性校验

- **OCR识别功能**
  - 简繁双引擎识别（<mcfile name="recognition.py" path="d:\hanziproject-副本\hanzi_app\recognition.py"></mcfile>）
  - 可信度比较算法
  - 图像预处理支持

### 扩展功能
- **数据导出**
  - ZIP打包下载（<mcsymbol name="download_file" filename="views.py" path="d:\hanziproject-副本\hanzi_app\views.py" startline="527" type="function"></mcsymbol>）
  - Excel报表生成
  
- **管理系统**
  - Django Admin定制（<mcfile name="admin.py" path="d:\hanziproject-副本\hanzi_app\admin.py"></mcfile>）
  - 搜索过滤（ID/汉字/拼音）
  - 排序功能（笔画数优先）

## 技术栈
| 类别        | 技术/工具                 |
|-----------|-----------------------|
| 后端框架    | Django 4.2            |
| 前端框架    | Bootstrap 5.3         |
| 数据库      | SQLite3               |
| OCR引擎    | EasyOCR               |
| 图像处理    | Pillow                |
| 部署       | ASGI                  |

## 安装与部署
### 开发环境配置
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
   - 设置`DEBUG = False`
   - 配置`ALLOWED_HOSTS`
   - 设置`SECRET_KEY`
2. 建议使用Nginx + uWSGI部署
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

3. **识别功能**：
   ```python
   # 示例调用代码
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

## 配置说明
关键配置项（`settings.py`）：
```python
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
UPLOAD_FOLDER = os.path.join(MEDIA_ROOT, 'uploads')
```

## API文档
### 汉字详情接口
**端点**：`/hanzi/<str:hanzi_id>/`  
**方法**：GET  
**返回**：HTML页面（<mcfile name="detail.html" path="d:\hanziproject-副本\templates\hanzi_app\detail.html"></mcfile>）

### 数据下载接口
**端点**：`/download/<str:filename>/`  
**方法**：GET  
**响应**：
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
MIT License (详见项目根目录LICENSE文件)
```

此README包含：
1. 从数据库模型到前端展示的完整架构说明
2. 关键代码模块的交叉引用
3. 开发部署的全流程指导
4. 系统设计的技术细节
5. 项目维护规范

需要补充实际部署信息时，请提供服务器配置细节。
