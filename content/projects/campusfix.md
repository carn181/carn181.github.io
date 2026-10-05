+++
title = "CampusFix"
date = 2026-07-30T00:00:00Z
period = "Jun–Jul 2026"
summary = "Android campus issue-reporting app for Georgia Tech CS 2340. Students report maintenance and safety issues; staff assign, update, and resolve them. Built with Java, MVVM, and Firebase."
tags = ["Java", "Android", "Firebase", "Firestore", "MVVM", "MapLibre", "JUnit"]
+++

### Overview

**CampusFix** is an Android app that streamlines how students report campus issues and how staff manage them. Students submit reports with location, category, priority, and description; staff assign issues, update status, add internal notes, and track analytics. Built with a team of 5 for Georgia Tech's **CS 2340: Objects and Design** (Summer 2026).

[github.com/Icygamer5/CS2340_S26_Team2](https://github.com/Icygamer5/CS2340_S26_Team2)

---

### My Contributions

I owned major pieces of the app across the full stack:

- **Staff dashboard & issue lifecycle**
  - Built `StaffActivity`, `StaffViewModel`, and `StaffRepository` so staff can view, assign, and change issue status.
  - Refactored `IssueUpdate` into a typed hierarchy (status change, assignment change, comment, staff note) and added `IssueUpdateManager` to unify updates across student and staff views.
  - Extended the `Issue` model with assignment fields and `isAssignedStaff()` to support staff-specific logic.

- **Discussion threads**
  - Designed a Reddit-style threaded comment system: `DiscussionMessage`, `DiscussionRepository`, `DiscussionManager`, `DiscussionViewModel`, and `DiscussionAdapter`.
  - Implemented tree-building logic for nested replies, plus edit/delete operations in `DiscussionViewModel`.

- **Authentication & account management**
  - Implemented login and create-account flows, `AuthRepository`, and `AccountValidator`.
  - Added profile features: change email, change password, delete account, and logout with cache clearing.
  - Added Arabic, Spanish, French, and Hindi translations.

- **Issue feed & card UI**
  - Built `IssueCardHelper` to render issue cards with status, priority, upvotes, and discussion threads across the feed and detail pages.
  - Connected upvote UI to the Firestore-backed model and refactored upvote logic into `IssueCardInteractions`.

- **Code quality & testing**
  - Set up SonarQube GitHub Actions and Checkstyle enforcement.
  - Wrote JUnit/Mockito tests for issue lifecycle, upvote logic, logout, and issue updates.
  - Unified JaCoCo coverage reporting for unit and instrumented tests.

---

### Tech Stack

| Layer | Technologies |
|---|---|
| Language | Java 17 |
| Architecture | MVVM with Android data binding |
| Backend / Auth | Firebase Authentication, Cloud Firestore, Firebase Realtime Database |
| Maps | MapLibre (geocoding via Nominatim) |
| Charts | MPAndroidChart |
| Testing | JUnit 4, Mockito, Espresso, JaCoCo |
| CI / Quality | GitHub Actions, SonarQube, Checkstyle |

---

### What I Learned

CampusFix gave me hands-on experience with Android's MVVM/data-binding lifecycle, designing Firebase schemas for real-time updates, and coordinating a multi-contributor codebase with strict style and coverage gates. The most valuable lesson was keeping UI logic decoupled from data logic: centralizing issue updates through `IssueUpdateManager` rather than letting views mutate model state directly made the staff and feed flows significantly easier to test and extend.
