```markdown
# Link2You - 多功能网站应用


基于 Flask 构建的多功能网站，集成用户管理、留言板、图片画廊及服务器监控功能。

![image](https://github.com/user-attachments/assets/90559273-996f-436f-a525-a43842fb2e15)

## 主要功能

### � 用户管理
- 注册/登录/退出
- 会话保持与安全验证

### 📝 留言板
- 实时发布评论
- 时间戳展示历史留言
![image](https://github.com/user-attachments/assets/dba17192-a77e-4b6e-a127-f13b275c8c2c)

### 🖼️ 图片画廊
- 图片上传至 `static/assets/gallery_pics`
- 自动渲染目录图片
- 点击下载功能
![image](https://github.com/user-attachments/assets/490c4931-f741-4aa5-84a7-0f8fbcc856b1)

### 📊 服务器状态监控
- 实时显示 CPU/内存/磁盘使用率
- SSL 证书检测
- 网络延迟测试
![image](https://github.com/user-attachments/assets/6603ac93-2711-457a-8fb2-d8abe1d6d061)

## 项目结构

```plaintext
Link2You/
├── app.py                  # Flask 主程序
├── Dockerfile              # Docker 构建配置
├── requirements.txt        # Python 依赖库
├── templates/              # Jinja2 模板
│   ├── base.html           # 基础布局模板
│   └── (各功能页面模板)...
└── static/
    ├── assets/             # 静态资源
    │   ├── gallery_pics/   # 用户上传图片存储
    │   ├── css/           # 样式表
    │   ├── js/            # 动态背景特效脚本
    │   ├── image/         #网页图片资源
    │   └── fromt/          #网页字体资源
```

## 🛠️ 快速开始

### 本地运行

1. **安装依赖**
```bash
pip install -r requirements.txt
```

2. **初始化数据库**
```python
# 在 Python 交互环境中执行
from app import app, db
with app.app_context():
    db.create_all()
```

3. **启动服务**
```bash
python app.py
```
➤ 访问 http://localhost:800

### Docker 部署
dockerfile需要先自己填写数据库服务器相关信息哦

![image](https://github.com/user-attachments/assets/ed8c451c-915f-469f-a285-9ea743fbdbdf)

1. **构建镜像**
```bash
docker build -t link2you-app .
```

2. **运行容器**
```bash
docker run -d -p 800:800 \
  -e DB_USER=prod_user \
  -e DB_PASSWORD=secure_pass \
  link2you-app
```

## ⚙️ 环境变量配置

| 变量名         | 必需 | 默认值       | 说明                 |
|----------------|------|-------------|----------------------|
| `DB_USER`      | 是   | -           | 数据库用户名         |
| `DB_PASSWORD`  | 是   | -           | 数据库密码           |
| `DB_HOST`      | 是   | localhost   | 数据库地址           |
| `DB_PORT=`     | 是   | 800         | 容器对外端口         |
| `DB_NAME=`     | 是   | -           | 数据库对应的表名     |

> 📌 生产环境务必修改数据库凭证！

## 📌 注意事项

1. **图片存储**：上传图片自动保存至 `static/assets/gallery_pics`，需确保目录写入权限
2. **数据库支持**：默认使用 MySQL，如需切换 MySQL/PostgreSQL：
   ```python
   # app.py 中修改数据库URI格式
   app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql+pymysql://user:pass@host/dbname'
   ```
3. **HTTPS 适配**：若部署生产环境，建议添加反向代理（Nginx/Apache）并配置 SSL

## 📜 开源协议
本项目采用 [MIT License](LICENSE) 开源授权
