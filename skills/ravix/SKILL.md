---
name: ravix
description: Run coding work on Ravix tracks (persistent cloud sandboxes at ravix.sh) through the ravix MCP server. Use when the user asks to start, prompt, follow, or close a Ravix track, or to hand work to a cloud agent.
---

# Ravix

## When to use

- The user asks to run a task on Ravix or in a cloud sandbox.
- The user asks about the state of a Ravix track or task.

## Instructions

1. Call `list_projects` to find the project. Use `repo` (`owner/name`) or `query` to filter.
2. Start the work:
   - Use `launch_task` with `project_id` (or `repo`), `prompt`, and a new `request_id`. It opens a track and queues the first prompt. It returns `track_id`, `thread_id`, `task_id`, `branch`, and `url`.
   - Or use `create_track`, then `send_prompt` with the `track_id`.
3. Follow the work with `wait_task` (waits up to 50 seconds per call) or `get_task` (one read). Repeat `wait_task` until the task is done or needs input. Give the user the track `url`.
4. To continue, call `send_prompt` on the same track.

## Rules

- Use a new `request_id` for each new action. Use the same `request_id` only to retry the same action.
- `close_track` is irreversible. It destroys the track's machine and all uncommitted or unpushed work on it. Call it only when the user asks. Use `require_merged: true` when the user wants to close only after the pull request is merged.
