### queries
---
https://github.com/gmr/queries

```py
session = queries.Session("postgresql://postgres@localhost:5432/postgres")

queries.uri("server-name", 5432, "dbname", "user", "pass")

import pprint
import queries

with queries.Session() as session:
  for row in session.query('SELECT * FROM names'):
    pprint.pprint(row)

import pprint
import queries
with queries.Session() as session:
  results = session.callproc('chr', [65])
  pprint.pprint(results.as_dict())


from tornado import gen, ioloop, web
import queries

class MainHandler(web.RequestHandler):
  def initalize(self):
    self.session = queries.TornadoSession()
    
  @gen.coroutine
  def get(self):
    results = yield self.session.query('SELECT * FROM names')
    self.finish({'data': results.items()})
    results.free()
    
application = web.Application([
  (r"/", MainHandler),
])

if __name__ == "__main__":
  application.listen(8888)
  ioloop.IOLoop.instance().start()

```

```sh
pip install queries

```

```
```
