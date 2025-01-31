Getting Started
redis-py requires a running Redis server, and Python 3.7+. See the Redis quickstart for Redis installation instructions.

redis-py can be installed using pip via pip install redis.

Quickly connecting to redis
There are two quick ways to connect to Redis.

Assuming you run Redis on localhost:6379 (the default)

import redis
r = redis.Redis()
r.ping()
