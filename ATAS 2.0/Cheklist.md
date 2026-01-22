This is a dual project development:
1. atas-pro is a professional platform to reduce tedious connection process like cold email and messy & unprofessional flow between student and industry expert which both act as demand and supply. This project modified from a FYP MPV to a highly performance & scalable platform.
2. atas-link is a community platform to replace "rednote" with a more niche pathway especially for university student. Whoever to manage the traffic is the key to turn into profit. Our idea is professional tool as a entry point and attracted student to sign in an account for the community platform for more exciting uni life & discussion around them. This is a whole new project and located in a monorepo with atas-pro which easy to manage and this project implement more advance technique like websocket, redis, queue. algorithm and so on which is a basic of a community.

### 三、 ATAS 2.0 冲刺清单（已完成 Docker & Redis）

#### ✅ 第一阶段：地基（已完成）

- Docker 容器化部署
    
- Redis 基础连接
    
- `profile_service` 的读写缓存 (Cache-Aside)
    

#### 🚀 第二阶段：异步与解耦 (当前最优先)

**目标：解决“前端转圈圈”问题，提升用户体验。**

- **核心技术：** **Celery** (Python 的任务队列王者)。
    
- **应用场景：**
    
    1. **注册/通知邮件：** 用户点完按钮马上跳转，邮件后台发。
        
    2. **AI 生成：** 现在的 AI 生成 Proposal 太慢了，必须异步化。
        
    3. **定期任务：** 每天凌晨自动给“快过期的活动”发提醒。
        

#### 🛡️ 第三阶段：安全与高可用 (大厂加分项)

**目标：防止系统被攻击，保证稳定性。**

- **核心技术：** **Redis Rate Limiter** (限流器)。
    
- **应用场景：** 限制每个 IP 每分钟只能请求 5 次 AI 接口（防止 API 费用爆炸）。
    

#### 🕸️ 第四阶段：复杂关系 (终极杀招)

**目标：做大厂级别的推荐系统。**

- **核心技术：** **Neo4j** (图数据库)。
    
- **应用场景：** “推荐你二度人脉里的专家”。
    

---

### 四、 马上开始：部署 Celery 实现“真异步”

既然你已经理解了 Redis，Celery 就是建立在 Redis 之上的最佳实践。

**请在 `atas-v2` 中执行以下步骤：**

#### 1. 修改 `requirements.txt`

添加 Celery 依赖：

Plaintext

```
celery
redis
```

#### 2. 创建 Celery 实例 (`backend/app/core/celery_app.py`)

这是“任务调度中心”。

Python

```
from celery import Celery
import os

# 使用你之前配置的 Redis URL
REDIS_URL = os.getenv("REDIS_URL", "redis://localhost:6379/0")

celery_app = Celery(
    "atas_worker",
    broker=REDIS_URL,   # 任务发到哪里（Redis）
    backend=REDIS_URL   # 结果存在哪里（Redis）
)

celery_app.conf.update(
    task_serializer="json",
    accept_content=["json"],
    result_serializer="json",
    timezone="Asia/Kuala_Lumpur",
    enable_utc=True,
)
```

#### 3. 定义一个异步任务 (`backend/app/tasks/email_tasks.py`)

这是“后台厨师要做的菜”。

Python

```
from app.core.celery_app import celery_app
import time
import logging

logger = logging.getLogger(__name__)

@celery_app.task
def send_registration_email_task(email: str, username: str):
    """
    模拟发送邮件的耗时任务
    """
    logger.info(f"📨 开始给 {email} 发送邮件...")
    # 模拟 SMTP 连接耗时 3秒
    time.sleep(3) 
    # 这里写真正的 Email 逻辑 (调用 SES/SendGrid/Gmail)
    logger.info(f"✅ 邮件已发送给 {username}!")
    return f"Email sent to {email}"
```

#### 4. 在 Router 中调用 (`backend/app/routers/auth_router.py`)

这是“服务员下单”。

Python

```
from app.tasks.email_tasks import send_registration_email_task

@router.post("/register")
def register(user: UserCreate, db: Session = Depends(get_db)):
    # ... (创建用户的数据库逻辑) ...
    
    # --- 关键改变 ---
    # 以前：await send_email(user.email)  <-- 会卡住 3秒
    # 现在：
    send_registration_email_task.delay(user.email, user.username) 
    # .delay() 会把任务扔进 Redis 瞬间返回，不卡顿！
    
    return {"message": "User registered successfully. Please check your email."}
```

#### 5. 启动 Worker (在终端)

FastAPI 只是发布任务，你需要另一个进程来执行任务。

Bash

```
# 在 backend 目录下运行
celery -A app.core.celery_app worker --loglevel=info
```

---

### 你的下一步行动

现在，你已经有了 Redis 缓存。 **建议你立刻实施上面的 Celery 代码。** 当你看到 Router 瞬间返回，而终端里的 Celery Worker 在 3 秒后打印出 `✅ 邮件已发送` 时，你就真正掌握了**分布式系统的解耦**。

这在大厂面试里，叫 **"Asynchronous Processing Architecture" (异步处理架构)**。这比只会写 CRUD 高级得多。准备好动手了吗？