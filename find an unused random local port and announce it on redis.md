---
title: find an unused random local port and announce it on redis
created: '2022-08-09T06:15:35.018Z'
modified: '2022-08-09T06:29:43.776Z'
---

# find an unused random local port and announce it on redis

issues were found when launching apps on fixed ports.

maybe you should create this entry inside your `lazero` package? no need for uploading to pypi, just keep it under `pyjom` and leave a local install script there.

make sure all services are going to launch after the `redis_service.service` target.

python to get unused port:
```python
def getUnusedLocalhostPort():
    """
    These were "Borrowed" from YCM.
    See https://github.com/Valloric/YouCompleteMe
    """
    sock = socket.socket()
    # This tells the OS to give us any free port in the range [1024 - 65535]
    sock.bind(("", 0))
    port = sock.getsockname()[1]
    sock.close()
    return port
```

install redis-py:
```bash
pip install redis
```

python send port to redis:
```python
import redis

r = redis.Redis(
    host='hostname',
    port=port, 
    password='password')
# open a connection to Redis
 
port = getUnusedLocalhostPort()
r.set('programPort', port)
value = r.get('programPort')
print(value)

```
