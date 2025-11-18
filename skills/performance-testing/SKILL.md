---
name: load-performance-testing
description: Master JMeter, k6, load testing, stress testing, and performance analysis.
---

# Load & Performance Testing

## JMeter Setup

```
1. Add Thread Group
2. Add HTTP Request Sampler
3. Add Listeners (View Results)
4. Configure load: Users, ramp-up, duration
5. Run test
6. Analyze results
```

## k6 Testing

```javascript
import http from 'k6/http';
import { check } from 'k6';

export let options = {
  stages: [
    { duration: '30s', target: 20 },
    { duration: '2m', target: 100 },
    { duration: '30s', target: 0 },
  ],
};

export default function() {
  let res = http.get('http://example.com');
  check(res, {
    'status is 200': (r) => r.status === 200,
    'response time < 500ms': (r) => r.timings.duration < 500,
  });
}
```

## Key Metrics

✅ Response time (p50, p95, p99)
✅ Throughput (req/sec)
✅ Error rate
✅ Resource usage (CPU, Memory)
✅ Concurrent users
