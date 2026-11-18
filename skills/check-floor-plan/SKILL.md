---
name: check-floor-plan
description: Import a measured drawing into an editable Planner 5D project and check the recognition result against the source measurements.
---

# Import a measured plan

Keep replies focused on the drawing, progress and saved project link. Retain file,
request and job IDs internally for recovery; show them only when the user requests
diagnostics. Run relevant account reads and progress checks without asking for
confirmation in chat, subject to Claude's tool permissions.
Report recognition progress briefly in chat and provide the saved project link
when ready. Do not open a widget for progress or completion; use the chooser only
when the user needs to select the original file.

For a new chat upload, omit `image.request_id`: the service generates a UUID and
returns `upload_request_id` and `recognition_request_id`. Pass the latter unchanged
as recognition's `request_id`. Renew an expired upload link with the returned
`upload_request_id` and identical metadata. The chooser also supplies its own
recognition ID. IDs persist across chats and restarts. Retain all arguments for a
retry, including the same file ID and scale hint. On `request_id_conflict`, use
`get_operation` to recover the earlier request and its recognition job. Explain
that an earlier request used different inputs. A new ID is appropriate only for
a distinct import requested by the user, never to blindly replay uncertain work.

1. Confirm the user's linked Planner 5D account. For a chat attachment, try code execution to locate its original PNG, JPEG or WebP file, measure its size and compute SHA-256. Call `create_chat_image_upload` with that metadata, omitting `image.request_id`, then PUT the raw file bytes to its returned URL using exactly `upload_headers`, without following redirects. That Authorization header is scoped to this upload; never substitute MCP or Planner credentials. Use the returned ready `file.id` and service-issued `recognition_request_id`. Keep credentials and IDs out of replies. If code execution cannot access the original or reach the upload URL, use the upload panel. Never call a file too large without measuring it against the 8 MiB limit. An existing owned input file can be reused directly.
2. Start the free standalone `start_floor_plan_recognition` workflow. It creates a new project and takes no Space ID. The separate `account_startPlanRecognition` operation spends credits for an explicitly requested Space; a failed standalone import must not trigger that paid operation.
3. Set a scale hint only for a measured horizontal or vertical segment with clear endpoints. Keep measured and inferred dimensions separate; report unreadable measurements as unknown.
4. Poll `get_floor_plan_recognition` with the original job ID. Retain the returned project hash and saved link when publication completes. Recover the original job after an uncertain result.
5. Open the resulting project in Planner 5D and ask the user to check room dimensions, openings and scale against the drawing. Report any discrepancy with its source measurement; this connector does not expose native room-editing commands.
