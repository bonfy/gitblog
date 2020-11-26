# [初尝FastAPI](https://github.com/bonfy/gitblog/issues/5)

FastAPI 可谓说目前Python Web Framework 中的当红炸子鸡，一直只闻其名，没有尝试过，今天抽空也尝试一把。

## 主页

* 官网： https://fastapi.tiangolo.com/
* Github： https://github.com/tiangolo/fastapi

## 安装
```cmd
$ pip3 install fastapi
$ pip3 install uvicorn # run as server

$ uvicorn main:app --reload

INFO:     Uvicorn running on http://127.0.0.1:8000 (Press CTRL+C to quit)
INFO:     Started reloader process [28720]
INFO:     Started server process [28722]
INFO:     Waiting for application startup.
INFO:     Application startup complete.
```

## 参考资料
* https://zhuanlan.zhihu.com/p/131625459

---

main.py
```py
# coding: utf-8

from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def home():
    return {'status': 'ok'}

if __name__ == "__main__":
    import uvicorn
    uvicorn.run(app, host="0.0.0.0", port=8000)
```


```cmd
$ uvicorn main:app --reload --host 0.0.0.0 --port 8000
```


Gunicorn

```cmd
$ pip3 install  gunicorn

$ gunicorn -w 4 -b 0.0.0.0:5000  manage:app -D

```