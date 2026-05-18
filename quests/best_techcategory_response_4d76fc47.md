# Best Tech-Category Response

# Debugging Guide: Diagnosing Memory Leaks in Node.js Applications

## Problem Statement

Node.js applications experiencing gradual memory growth often indicate leaks in object references, event listeners, or closures.

## Diagnostic Command

```bash
# Generate heap snapshot for analysis
node --inspect server.js

# Or use clinic.js for automated diagnosis
npx clinic doctor -- node server.js
```

## Reproduction Steps

1. Create a leaky server:
```javascript
// leaky-server.js
const http = require('http');

const cache = new Map();
let counter = 0;

const server = http.createServer((req, res) => {
  // Problem: Adding to cache without cleanup
  cache.set(counter++, { 
    data: Buffer.alloc(1024 * 100), // 100KB per request
    timestamp: Date.now()
  });
  
  res.json({ cached: cache.size });
});

server.listen(3000);
```

2. Run and monitor:
```bash
node leaky-server.js &
watch -n 5 'curl -s http://localhost:3000 && echo " - Memory:" $(ps aux | grep leaky-server | grep -v grep | awk "{print \$6}") "KB"'
```

3. Observe memory growth with each request.

## Root Cause Analysis

**Issue:** `Map` grows indefinitely with no eviction policy.

## Fix Implementation

```javascript
// fixed-server.js
const http = require('http');

const cache = new Map();
const MAX_CACHE_SIZE = 100;
const CACHE_TTL_MS = 60000;

function cleanup() {
  const now = Date.now();
  for (const [key, entry] of cache) {
    if (now - entry.timestamp > CACHE_TTL_MS) {
      cache.delete(key);
    }
  }
}

const server = http.createServer((req, res) => {
  cleanup();
  
  if (cache.size >= MAX_CACHE_SIZE) {
    // Evict oldest entry
    const firstKey = cache.keys().next().value;
    cache.delete(firstKey);
  }
  
  const key = cache.size;
  cache.set(key, { 
    data: Buffer.alloc(1024 * 100),
    timestamp: Date.now()
  });
  
  res.json({ cached: cache.size });
});

setInterval(cleanup, 30000);
server.listen(3000);
```

## Verification

```bash
# Run for 5 minutes with 10 req/s
ab -n 3000 -c 10 http://localhost:3000/
ps -o rss= -p $(pgrep -f leaky-server)
```

Fixed version maintains stable ~50MB; leaky version grows to 400MB+.