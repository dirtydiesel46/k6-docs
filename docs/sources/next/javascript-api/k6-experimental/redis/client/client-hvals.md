---
title: 'Client.hvals(key)'
excerpt: 'Returns all values of the hash stored at `key`.'
---

# Client.hvals(key)

Returns all values of the hash stored at `key`.

### Parameters

| Parameter | Type   | Description                                |
| :-------- | :----- | :----------------------------------------- |
| `key`     | string | key holding the hash to get the fields of. |

### Returns

| Type                | Resolves with                                                         | Rejected when                                                      |
| :------------------ | :-------------------------------------------------------------------- | :----------------------------------------------------------------- |
| `Promise<string[]>` | On success, the promise resolves with the list of values in the hash. | If the hash does not exist, the promise is rejected with an error. |

### Example

{{< code >}}

```javascript
import redis from 'k6/experimental/redis';

// Instantiate a new redis client
const redisClient = new redis.Client('redis://localhost:6379');

export default async function () {
  await redisClient.hset('myhash', 'myfield', 'myvalue');
  await redisClient.hset('myhash', 'myotherfield', 'myothervalue');

  const values = await redisClient.hvals('myhash');
  if (values.length !== 2) {
    throw new Error('myhash should have 2 values');
  }

  console.log(`myhash has values ${values}`);
}
```

{{< /code >}}
