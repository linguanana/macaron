# Interview Prep Master

This file is a cleaned-up Markdown version for check-in and future reuse.
It is meant to be easy for both humans and AI tools to read.

## Why Markdown

- easier to organize and scan
- better for git history and check-in
- easier for AI tools to read later
- easier to keep growing over time

## Core Speaking Questions

### 1. Tell me about yourself.

What to look for:
- 30 to 60 seconds
- Zoom + Amazon
- backend / distributed systems / APIs / OAuth
- what he wants next

### 2. Tell me about a production issue you debugged.

What to look for:
- symptom
- investigation
- root cause
- fix
- follow-up / prevention

Helpful follow-ups:
- What was the symptom first?
- How did you narrow it down?
- What was the fix?
- What changed afterward?

### 3. Can you walk me through the S3 to MySQL migration?

What to look for:
- why S3 was not enough
- why MySQL helped
- rollout / migration safety
- impact

Helpful follow-ups:
- What problem were you trying to solve?
- Why was MySQL a better fit?
- How did you avoid breaking production?

## Practical Coding Questions

### Auth / Backend State

- Token Manager
- Session Store
- Login Failure Tracker
- Scope / Permission Validator

### API / Request Handling

- API Rate Limiter
- Request Deduplicator
- Webhook Retry Queue
- Idempotency Key Tracker
- API Request Validator
- API Quota Tracker

### Data Structure / Interview Standard

- Merge Logs from N Servers
- LRU Cache
- Top K Frequent Elements

## API-Focused Questions

These are useful because many teams are API-heavy, not just auth-heavy.

### Speaking / Design-Light

- How would you design an API rate limiter?
- How would you prevent duplicate requests in a payment-style API?
- How would you design retry handling for webhook delivery?
- How would you validate and reject bad API requests?
- How would you think about versioning for public APIs?

### Practical Coding

#### API Rate Limiter

Prompt:
Implement a simple per-user API rate limiter.

Support:
- allow(userId, timestamp)

Rule:
- allow at most N requests within a fixed time window

What it tests:
- state modeling
- time-window logic
- per-user tracking

#### Request Deduplicator

Prompt:
Implement a request deduplicator.

Support:
- recordRequest(requestId, timestamp)
- isDuplicate(requestId, timestamp)

Rule:
- if the same requestId appears again within the dedup window, treat it as duplicate

What it tests:
- hashmap
- time-based cleanup
- idempotency thinking

#### Webhook Retry Queue

Prompt:
Implement a simple webhook retry queue.

Support:
- enqueue(eventId, timestamp)
- markSuccess(eventId)
- getReadyEvents(currentTime)

What it tests:
- queue thinking
- retry state
- practical backend workflow

## Common Backend Objects and Fields

### LogEntry

Fields:
- `timestamp`
- `message`
- `serverId`

Represents:
- one log event from one server

### LoginTracker

Fields:
- `userId`
- `failed timestamps`
- maybe lock-related state if needed

Represents:
- per-user login failure state

### SessionRecord

Fields:
- `sessionId`
- `userId`
- `expiryTime`
- `invalidated` / `active`

Represents:
- one user session

### TokenRecord

Fields:
- `token`
- `userId`
- `expiryTime`
- `revoked`

Represents:
- one auth token and its validation state

### RateLimitRecord

Fields:
- `userId` or `clientId`
- `request timestamps`
- `window size`
- `limit`

Represents:
- request history or counters for rate limiting

### RequestRecord

Fields:
- `requestId`
- `payload hash`
- `createdAt`
- `status`

Represents:
- one tracked request for deduplication or retry handling

### CacheNode

Fields:
- `key`
- `value`
- `prev`
- `next`

Represents:
- one node in a doubly linked list for cache ordering

### HeapEntry

Fields:
- `timestamp` or `priority`
- `source index` / `server index`
- `item index`
- object reference if needed

Represents:
- one candidate item inside a heap

## Before Coding

Before writing code, always explain:

1. what classes or functions you need
2. what fields each object should have
3. what data structure you will use
4. what the flow of the solution is

This is important because many mistakes come from coding before the problem is fully understood.

## Best Questions To Reuse Often

- Tell me about yourself.
- Tell me about a production issue you debugged.
- Can you walk me through the S3 to MySQL migration?
- Login Failure Tracker
- Session Store
- API Rate Limiter

