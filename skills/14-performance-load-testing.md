---
name: performance-load-testing-jmeter-k6
description: Master performance testing, load testing with JMeter and k6, stress testing, and performance optimization.
---

# Performance & Load Testing

## JMeter

```
1. Add Thread Group
2. Configure HTTP Samplers
3. Add Listeners
4. Run test
5. Analyze results
```

## k6

```javascript
import http from 'k6/http'
export let options = {
  stages: [
    {duration: '30s', target: 20}
  ]
}
export default function() {
  http.get('http://example.com')
}
```

## Metrics

- Response time (p50, p95, p99)
- Throughput (req/sec)
- Error rate
- Resource usage

## Testing Types

✅ Load testing
✅ Stress testing
✅ Spike testing
✅ Soak testing
