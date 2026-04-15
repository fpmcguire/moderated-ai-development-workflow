# QA: Step 01

**Project:** Frontend Saved Views  
**Step:** 01 — SavedView Data Model and REST API  
**Tester:** Sam Okafor  
**Test Date:** 2026-01-20

---

## Summary

**Result:** Pass

All test cases pass. The API behaves as specified. No defects found.

---

## Test Environment

| Item           | Value                                                   |
| -------------- | ------------------------------------------------------- |
| Environment    | Local dev with Docker Compose                           |
| Runtime        | Node.js 20.x                                            |
| Database state | Fresh migration applied; seeded with test user accounts |
| Dependencies   | All services running via `docker compose up`            |

---

## Test Cases

| #     | Description                          | Steps                                                            | Expected Result                                   | Actual Result                        | Status |
| ----- | ------------------------------------ | ---------------------------------------------------------------- | ------------------------------------------------- | ------------------------------------ | ------ |
| TC-01 | Create a SavedView                   | POST `/api/saved-views` with valid payload as authenticated user | 201 Created with SavedView JSON                   | 201 Created with correct JSON        | Pass   |
| TC-02 | List SavedViews for a list view      | GET `/api/saved-views?listViewId=orders` as authenticated user   | 200 OK with array of user's views for `orders`    | Correct array returned               | Pass   |
| TC-03 | List returns only own views          | GET `/api/saved-views?listViewId=orders` as different user       | 200 OK with empty array                           | Empty array returned                 | Pass   |
| TC-04 | Enforce 50-view limit                | POST 51st SavedView for same user and listViewId                 | 422 Unprocessable Entity                          | 422 returned with clear message      | Pass   |
| TC-05 | Enforce name length                  | POST with name of 101 characters                                 | 422 Unprocessable Entity                          | 422 returned                         | Pass   |
| TC-06 | Rename a SavedView                   | PATCH `/api/saved-views/:id` with new name                       | 200 OK with updated name                          | Correct response                     | Pass   |
| TC-07 | Pin a SavedView                      | PATCH `/api/saved-views/:id` with `isPinned: true`               | 200 OK with `isPinned: true`                      | Correct response                     | Pass   |
| TC-08 | Cannot update another user's view    | PATCH with valid ID but different user auth                      | 403 Forbidden                                     | 403 returned                         | Pass   |
| TC-09 | Delete a SavedView                   | DELETE `/api/saved-views/:id` as owner                           | 204 No Content                                    | 204 returned; record removed from DB | Pass   |
| TC-10 | Cannot delete another user's view    | DELETE with valid ID but different user auth                     | 403 Forbidden                                     | 403 returned                         | Pass   |
| TC-11 | userId not trusted from request body | POST with `userId` in body set to another user's ID              | View created with session userId, not body userId | Session userId used correctly        | Pass   |

---

## Defects

No defects found.

---

## Regression Check

- [x] Existing tests continue to pass (ran `npm test` — all 214 pre-existing tests pass)
- [x] No unintended side effects observed in adjacent features

---

## Notes

TC-11 was added by the tester as a security-focused case not listed in STEP.md. It passes — the server correctly ignores the `userId` field in the request body. Recommend adding this case to the Level 2 quality gate checklist for future API steps.

---

MOD-W v2.1.0 · Moderated AI Development Workflow · https://github.com/fpmcguire/moderated-ai-development-workflow
