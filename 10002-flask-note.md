# gunicorn 的使用
- pip install gunicorn  
- 命令行启动 gunicorn -b "0.0.0.0:8000" -w N manage:app
这样会启动N个进程  
