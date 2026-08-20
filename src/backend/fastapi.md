# fastapi

## 安装与运行

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install fastapi "uvicorn[standard]"
```

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/health")
def health():
    return {"status": "ok"}
```

保存为 `main.py` 后执行 `uvicorn main:app --reload`。开发时可访问 `/docs` 查看 OpenAPI 文档。请求体应使用 Pydantic 模型校验，配置和密钥从环境变量读取。

## 请求模型

```python
from pydantic import BaseModel

class UserCreate(BaseModel):
    name: str
    email: str

@app.post("/users", status_code=201)
def create_user(user: UserCreate):
    return user
```

## 常用命令

```powershell
uvicorn main:app --reload --port 8000
uvicorn main:app --host 0.0.0.0 --port 8000
pip freeze > requirements.txt
pip install -r requirements.txt
```

## 经验总结

1. `--reload` 只用于本地开发，生产环境使用进程管理器和多个 worker。
2. 使用 `HTTPException` 返回明确的 HTTP 错误码，不要把 Python 异常原样返回给客户端。
3. 通过依赖注入管理数据库会话和认证信息，确保请求结束后释放连接。
