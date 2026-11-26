---
name: latency-timing
description: Find where the time goes in a slow request (API call, SSE stream, database query, LLM or Dify call) by adding timestamped checkpoints on both the frontend and the backend. Use when investigating latency or slow responses.
---

# Find the slow step with timing checkpoints

1. Pick the slow path end to end, from the user action in the browser or app to the last byte the backend sends.
2. At each step, log the elapsed time since a single start time, with a prefix you can grep for:
   ```typescript
   const startTime = Date.now();
   console.log(`[CHAT] request sent`);
   // ... operation ...
   console.log(`[CHAT] first token: +${Date.now() - startTime}ms`);
   ```
   Do the same on the server (with the elapsed milliseconds from the request's start).
3. Log only timings, ids and step names. Never log message text or other conversation content: in these products it is health-related user data.
4. Run the slow case, line up the frontend and backend logs, and find the largest gap between two checkpoints. That gap is the bottleneck.
5. Remove the checkpoints when done, or keep them behind a debug flag.

For a slow LLM step, check what actually served the request before optimizing code. A 20-second delay was once a Dify app running an unpublished GPT workflow instead of the faster Qwen model.
