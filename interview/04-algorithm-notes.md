# 🚀 Algorithm CHEAT SHEET: PATTERNS & FUNCTIONS

This file is a quick reminder for common interview data structures and patterns.

## 1. HashMap (The "State Manager")
Use: Fast lookup (O(1)), tracking state by user/token/session.
Key Functions:
- getOrDefault(key, default): Perfect for counters or trackers.
- putIfAbsent(key, val): Useful for initialization.
- containsKey(key): Check for existence before processing.

Common Examples:
- Token Manager: map.get(token) -> returns UserRecord.
- Deduplicator: map.containsKey(requestId) -> skip if true.
- Counter: map.put(id, map.getOrDefault(id, 0) + 1).

---

## 2. Heap / Priority Queue (The "Ranker")
Use: Smallest/largest element, Top K, merging sorted streams.
Key Functions:
- offer(val) / poll(): Add and remove the top priority item.
- peek(): Inspect the top without removing.
- Custom Comparator: (a, b) -> a.val - b.val (Min-Heap).

Common Examples:
- Log Merger: Keep the earliest timestamp from N server logs in a Min-Heap.
- Top K Frequent: Use a Min-Heap of size K to keep the largest elements.

---

## 3. Queue / Deque (The "Window Tracker")
Use: FIFO (First-In-First-Out), processing in order, time windows.
Key Functions:
- offerLast(val) / pollFirst(): Standard Queue operations.
- peekFirst(): Check the oldest event in a time window.

Common Examples:
- Rate Limiter: Store request timestamps; remove those older than (now - window_size).
- Retry Queue: Push failed webhooks to the back; process from the front.

---

## 4. Sliding Window (The "Event Filter")
Logic Pattern:
1. add(right_item) to window.
2. while (condition_violated): remove(left_item), left++.
3. update_result().

Common Examples:
- Login Failure Tracker: "Has this user failed 5 times in the last 10 minutes?"

---

## 5. Doubly Linked List + HashMap (LRU Cache)
Use: O(1) removal and O(1) update of most/least recently used items.
Key Functions:
- moveToHead(node): Mark as recently used.
- popTail(): Evict the oldest item when cache is full.

---

## 6. Exponential Backoff (Retry Logic)
Use when: A background task fails and needs to be retried without crashing the system.
Logic: `delay = 2 ^ retry_count`.
Common Examples:
- Webhook retry queue.
- Failed payment processing.

## 7. Distributed Lock (Concurrency Control)
Use when: Multiple servers want to update the same resource (e.g., User Balance).
Logic:
1. Acquire: `setnx lock_key unique_owner_id EX 30`
2. Release: Only if `current_owner == my_owner_id`.
Common Examples:
- Inventory update in e-commerce.
- Wallet balance transactions.

---

# 🛠️ BACKEND OBJECT FIELDS & LOGIC

## LogEntry
- timestamp (Long): Primary sort key for heaps.
- serverId (String): Source identifier.
- message (String): Content.

## RateLimitRecord
- clientId (String): Target of the limit.
- requestTimestamps (Queue<Long>): The window history.
- Logic: while(q.peek() < now - 60s) q.poll(); return q.size() < limit;

## SessionRecord
- sessionId (String)
- expiryTime (Long): Use to trigger clean-up.
- isValid (Boolean): Quick revocation flag.

## RequestRecord (Idempotency)
- requestId (String): Unique key from client.
- status (PENDING, COMPLETED, FAILED).
- responsePayload (String): Cached response for duplicate requests.

---

## 💡 MENTAL TRIGGERS
- Top K? -> Heap.
- Recent X minutes? -> Deque + Sliding Window.
- O(1) Lookup? -> HashMap.
- Already Sorted? -> K-Way Merge (don't re-sort!).
- Deduplication? -> Request ID in a Map.


---
