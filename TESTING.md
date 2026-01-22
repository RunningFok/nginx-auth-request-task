# Testing Steps for Nginx and Traefik

## Setup

**Terminal 1:** Start services
```bash
docker compose up
```

**Terminal 2:** Run test commands (keep Terminal 1 open to view logs)

## Test Cases

### Test 1: Valid Token
```bash
curl -v -H "x-pretest: valid-token" http://localhost:8080/health
```
**Expected:** `200 OK`

### Test 2: Valid Token, 404 Endpoint
```bash
curl -v -H "x-pretest: valid-token" http://localhost:8080/404
```
**Expected:** `404 Not Found`

### Test 3: Invalid Token
```bash
curl -v -H "x-pretest: wrong-token" http://localhost:8080/health
```
**Expected:** `401 Unauthorized`

### Test 4: Missing Header
```bash
curl -v http://localhost:8080/health
```
**Expected:** `401 Unauthorized`

## Quick Test (All at Once)

```bash
echo "Test 1:" && curl -s -o /dev/null -w "%{http_code}\n" -H "x-pretest: valid-token" http://localhost:8080/health
echo "Test 2:" && curl -s -o /dev/null -w "%{http_code}\n" -H "x-pretest: valid-token" http://localhost:8080/404
echo "Test 3:" && curl -s -o /dev/null -w "%{http_code}\n" -H "x-pretest: wrong-token" http://localhost:8080/health
echo "Test 4:" && curl -s -o /dev/null -w "%{http_code}\n" http://localhost:8080/health
```

**Expected:** `200`, `404`, `401`, `401`
