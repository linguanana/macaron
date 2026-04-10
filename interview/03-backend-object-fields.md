# Backend Object Fields

This file is a cheat sheet for common backend objects.

## LogEntry

Fields:
- `timestamp`
- `message`
- `serverId`

Represents:
- one log event from one server

## LoginTracker

Fields:
- `userId`
- `failed timestamps`
- maybe lock-related state if needed

Represents:
- per-user login failure state

## SessionRecord

Fields:
- `sessionId`
- `userId`
- `expiryTime`
- `invalidated` / `active`

Represents:
- one user session

## TokenRecord

Fields:
- `token`
- `userId`
- `expiryTime`
- `revoked`

Represents:
- one auth token and its validation state

## RateLimitRecord

Fields:
- `userId` or `clientId`
- `request timestamps`
- `window size`
- `limit`

Represents:
- request history or counters for rate limiting

## RequestRecord

Fields:
- `requestId`
- `payload hash`
- `createdAt`
- `status`

Represents:
- one tracked request for deduplication or retry handling

## CacheNode

Fields:
- `key`
- `value`
- `prev`
- `next`

Represents:
- one node in a doubly linked list for cache ordering

## HeapEntry

Fields:
- `timestamp` or `priority`
- `source index` / `server index`
- `item index`
- object reference if needed

Represents:
- one candidate item inside a heap
