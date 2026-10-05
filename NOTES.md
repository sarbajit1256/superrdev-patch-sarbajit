# Notes

## Summary of Changes

I found and fixed four issues while running and browsing the application:

1. Fixed the task search/status filtering query by grouping the title and description conditions with parentheses. This ensures the status filter is applied to the complete search result.
2. Fixed stale frontend pagination state. Changing the search query or status now resets pagination to the first page.
3. Removed unnecessary artificial server-side delay caused by complexity/weight calculation and `Thread.sleep()`, which was increasing request latency and blocking the server thread.
4. Moved task pagination from in-memory Java `List`/`subList()` processing to database-level pagination using Spring Data JPA `Pageable` and `Page<Task>`.

## What I Chose Not to Change

I observed that task IDs were displayed in descending order. The repository explicitly orders tasks by `created_at DESC`, which appears intentional because it shows the newest tasks first. I did not change this behavior without a confirmed product requirement.

I also avoided unrelated refactoring because this was a focused patch exercise.

## Biggest Remaining Risk

The biggest remaining risk is pagination behavior under larger datasets and different combinations of search, status, and page changes. Additional testing with realistic data volume would help verify both performance and edge cases.

## Tools / AI Used

I used the local application, browser developer tools, IDE/code navigation, and database/query inspection to investigate the issues. I used ChatGPT to help explain SQL operator precedence and reason about pagination and query behavior. I verified the changes against the application rather than relying only on AI-generated suggestions.