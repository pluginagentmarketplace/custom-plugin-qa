---
name: performance-testing
description: Master JMeter, k6, load testing, stress testing, performance profiling, bottleneck analysis.
---

# Performance & Load Testing

## Quick Start - k6

```javascript
import http from 'k6/http';
import { check } from 'k6';

export let options = {
  stages: [
    { duration: '30s', target: 20 },
    { duration: '1m30s', target: 100 },
    { duration: '20s', target: 0 },
  ],
};

export default function() {
  let res = http.get('http://localhost:3000');
  check(res, {
    'status is 200': (r) => r.status === 200,
    'response time < 500ms': (r) => r.timings.duration < 500,
  });
}
```

## Tools

### JMeter
- Load testing
- Protocol support (HTTP, FTP, JDBC)
- Assertions & extractors
- Distributed testing

### k6
- Modern, scriptable
- Performance metrics
- Real-time results
- Cloud integration

### Locust
- Python-based
- User behavior simulation
- Distributed load generation

## Load Testing Types

### Load Testing
- Normal user load
- Response time measurement
- Throughput analysis

### Stress Testing
- Beyond normal capacity
- Find breaking point
- Resource limits

### Spike Testing
- Sudden traffic increase
- System recovery

### Soak Testing
- Long-duration load
- Memory leaks
- Resource degradation

## Metrics

### Response Time
- P50, P95, P99 percentiles
- Min/Max/Average
- Distribution analysis

### Throughput
- Requests per second
- Transaction success rate
- Error rates

### Resource Usage
- CPU utilization
- Memory consumption
- Network bandwidth
- Disk I/O

## Best Practices

✅ Establish baselines
✅ Load test realistic scenarios
✅ Monitor system resources
✅ Test early & often
✅ Analyze trends
✅ Document assumptions
✅ Share results widely

## Related Skills
- Performance & Load Testing
- Quality Metrics & Reporting
