# Backend Object Fields

This file is a cheat sheet for common backend objects.

## LogEntry

Fields:
- `timestamp`
- `message`
- `serverId`

Represents:
- one log event from one server

Key Logic:
- Used as the base object in a Min-Heap for K-Way Merging. Sort by `timestamp` ascending.

## LoginTracker

Fields:
- `userId`
- `failed timestamps`
- maybe lock-related state if needed

Represents:
- per-user login failure state

Logic Functions:
- isLocked(): Returns (now < lockUntil).
- recordFailure(now): Add 'now' to queue; if (count in last 10m > limit), set lockUntil = now + 15m.

## SessionRecord

Fields:
- `sessionId`
- `userId`
- `expiryTime`
- `invalidated` / `active`

Represents:
- one user session

Logic Functions:
- isValid(): Returns (status == Active && now < expiryTime).
- refresh(duration): Set expiryTime = now + duration (Extend session).

## TokenRecord

Fields:
- `token`
- `userId`
- `expiryTime`
- `revoked`

Represents:
- one auth token and its validation state

Logic Functions:
- isLocked(): Returns (now < lockUntil).
- recordFailure(now): Add 'now' to queue; if (count in last 10m > limit), set lockUntil = now + 15m.

## RateLimitRecord

Fields:
- `userId` or `clientId`
- `request timestamps`
- `window size`
- `limit`

Represents:
- request history or counters for rate limiting

Logic Functions:
- isAllowed(now):
    1. while (q.peekFirst() < now - windowSize) q.pollFirst(); // Slide window
    2. if (q.size() < limit) { q.addLast(now); return true; }
    3. return false;

## RequestRecord

Fields:
- `requestId`
- `payload hash`
- `createdAt`
- `status`

Represents:
- one tracked request for deduplication or retry handling

Logic Functions:
- checkAndProcess():
    - If Success: Return responseCache.
    - If Pending: Return "Processing" error (to avoid double-work).
    - If None: Set to Pending and start processing.

## CacheNode

Fields:
- `key`
- `value`
- `prev`
- `next`

Represents:
- one node in a doubly linked list for cache ordering

Logic Functions:
- detach(): Update prev.next = next and next.prev = prev.
- promote(): detach() then move to Head (mark as recently used).

## HeapEntry

Fields:
- `timestamp` or `priority`
- `source index` / `server index`
- `item index`
- object reference if needed

Represents:
- one candidate item inside a heap

Logic Functions:
- fetchNext(): After poll(), use sourceIndex to fetch the next item from that specific stream to maintain the heap size.


## RetryTask (Reliability)

Fields:
- `taskId`
- `payload`
- `retryCount` (current attempt)
- `nextRunTime` (timestamp to trigger)

Represents:
- A failed job that needs to be retried using Exponential Backoff.

Logic Functions:
- scheduleNext(): retryCount++; nextRunTime = now + (base * 2^retryCount).
- shouldDrop(): Returns (retryCount > MAX_RETRIES).

## DistributedLock (Fencing)

Fields:
- `lockKey`
- `ownerId` (UUID to verify who owns the lock)
- `ttl` (time-to-live to prevent deadlocks)

Represents:
- A shared lock across multiple servers to prevent race conditions.

Logic Functions:
- acquire(id, duration): SET lockKey id NX EX duration (Only set if it doesn't exist).
- safeRelease(id): ONLY delete if (current_owner == my_id). This prevents accidentally releasing a lock acquired by someone else after yours expired.
