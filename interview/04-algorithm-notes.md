# Algorithm Notes

This file is a quick reminder for common interview data structures and patterns.

## HashMap

Use when you need:
- fast lookup by key
- state by user / token / session / request id

Common examples:
- token manager
- session store
- login failure tracker
- request deduplicator

## Heap / Priority Queue

Use when you need:
- the smallest or largest current item
- top k
- merge multiple sorted sources

Common examples:
- merge logs from N servers
- top k frequent elements

## Queue / Deque

Use when you need:
- remove old items from the front
- process items in order
- maintain a time window

Common examples:
- login failure tracker
- rate limiter
- webhook retry queue

## Sliding Window

Use when the rule depends on:
- recent events
- time windows
- fixed-size or moving windows

Common examples:
- login failure tracker
- API rate limiter

## Doubly Linked List

Use when you need:
- O(1) remove
- O(1) insert
- ordering that changes often

Common examples:
- LRU cache

## K-Way Merge

Idea:
- if multiple sources are already sorted
- do not sort everything again
- keep one candidate from each source in a heap

Common examples:
- merge logs from N servers
