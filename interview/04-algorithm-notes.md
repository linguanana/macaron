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

## 8. Binary Tree (DFS / BFS)
Use when: Data is shaped like parent -> left child / right child.

Common fields:
- value
- left
- right

Key idea:
- A binary tree node has at most two children.
- This is different from a graph, where a node can have many neighbors.

DFS patterns:

Preorder:
1. visit node
2. dfs(left)
3. dfs(right)

Inorder:
1. dfs(left)
2. visit node
3. dfs(right)

Postorder:
1. dfs(left)
2. dfs(right)
3. visit node

BFS pattern:
1. put root in queue
2. while queue is not empty:
   - pop front
   - visit node
   - add left child if exists
   - add right child if exists

Common examples:
- max depth of binary tree
- check if tree is balanced
- level order traversal
- validate binary search tree
- find a value in a tree

Mental trigger:
- If the problem says `left` and `right`, think binary tree.
- If the problem says dependencies / neighbors / services, think graph.

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

## 9. Two Pointers (The "Index Walker")
Use: Sorted arrays, palindrome checks, pair problems, and merging two streams.

Common patterns:
- Opposite ends: `left = 0`, `right = n - 1`, move inward.
- Same direction (fast/slow): compact arrays or detect cycles.
- Two inputs: move pointer in one/both lists until both are exhausted.

Template:
```python
left, right = 0, len(arr) - 1
while left < right:
    # problem-specific logic
    # move left, right, or both
```

---

## 10. Prefix Sum (The "Range Sum Accelerator")
Use: Frequent subarray sum queries.

Key idea:
- `prefix[i] = nums[0] + ... + nums[i]`
- Sum of subarray `i..j` = `prefix[j] - prefix[i - 1]` (if `i > 0`)

Template:
```python
prefix = [nums[0]]
for i in range(1, len(nums)):
    prefix.append(prefix[-1] + nums[i])
```

---

## 11. Linked List Core Moves
Use: Pointer manipulation, in-place structural updates.

Singly linked list:
- Insert after `prev`: `node.next = prev.next; prev.next = node`
- Delete after `prev`: `prev.next = prev.next.next`

Fast/slow pointer:
- Middle node, cycle detection, split list problems.

Reverse list (iterative):
```python
prev, curr = None, head
while curr:
    nxt = curr.next
    curr.next = prev
    prev, curr = curr, nxt
head = prev
```

---

## 12. Monotonic Stack / Queue
Use: Next greater/smaller element, window max/min, stock-span style problems.

Rules:
- Increasing stack: pop while top `>= current`.
- Decreasing stack: pop while top `< current`.
- Although nested loops appear, total is O(n) amortized.

---

## 13. Graph Essentials (DFS/BFS)
Use: Connectivity, components, shortest path in unweighted graphs.

Representations:
- Edge list
- Adjacency list (most common in interviews)
- Adjacency matrix
- Matrix-as-graph (grid problems)

Core rules:
- Always track `seen`/`visited` to avoid revisits.
- DFS explores deep; BFS explores level-by-level.
- Use BFS for shortest path in unweighted graphs.

---

## 14. Binary Search (Boundaries Matter)
Use: Sorted search space or monotonic condition.

Standard search:
```python
left, right = 0, len(arr) - 1
while left <= right:
    mid = (left + right) // 2
    if arr[mid] == target:
        return mid
    if arr[mid] > target:
        right = mid - 1
    else:
        left = mid + 1
return left  # insertion point
```

Duplicate-aware variants:
- Leftmost position: shrink right when `arr[mid] >= target`.
- Rightmost insertion point: shrink right only when `arr[mid] > target`.

---

## 15. Backtracking (Build + Undo)
Use: Enumerate all valid combinations/permutations/subsets.

Pattern:
1. Choose
2. Recurse
3. Undo choice

Skeleton:
```python
def backtrack(curr):
    if base_case:
        ans.append(curr.copy())
        return
    for choice in choices:
        apply(choice, curr)
        backtrack(curr)
        undo(choice, curr)
```

---

## 16. Dynamic Programming (State + Transition)
Use: Overlapping subproblems + optimal substructure.

Checklist:
- Define state: what does `dp[i]` (or `dp[state]`) mean?
- Define recurrence: how current answer comes from smaller states.
- Define base cases.
- Choose top-down (memoization) or bottom-up (tabulation).

Example idea:
- Min Cost Climbing Stairs:
  - `dp[i] = min(dp[i-1] + cost[i-1], dp[i-2] + cost[i-2])`

