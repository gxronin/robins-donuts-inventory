ROBIN'S DONUTS — INVENTORY TRACKER
Personal Project Summary
================================================================

OVERVIEW
--------
A real-time inventory management app I built for the donut shop I work
at, to replace manual stock-checking with a shared, mobile-friendly
system. Staff use it daily on phones at the counter to track stock,
get low-stock alerts, and generate supplier order lists — with every
device staying in sync automatically.

This was a self-directed project: I identified the actual problem
(inconsistent manual inventory tracking across shifts), scoped the
features based on real workflow needs, built and deployed it, then
iterated based on live feedback from staff actually using it day to
day — including debugging a real production issue with the database
connection after it went live.


SKILLS / TECH USED
---------------------
- React + Vite — frontend app structure and build tooling
- Firebase Firestore — real-time, multi-device data sync (no custom
  backend needed)
- Responsive / mobile-first UI design — built for one-handed counter use
- Netlify — deployment and static hosting
- Debugging real-time sync & network issues in a live production app
- Iterative feature development based on direct user (staff) feedback


KEY FEATURES
-------------
- Live shared inventory — every device sees the same stock counts,
  updated instantly when anyone makes a change
- Color-coded low-stock alerts (OK / Watch / Low / Out of Stock) based
  on a configurable threshold per item
- Full CRUD on inventory items — add, edit (name/category/unit/quantity/
  threshold), and delete (with a confirmation step to prevent mistakes)
- One-tap order list generation — auto-suggests reorder quantities,
  fully editable before export, downloadable as .txt or .csv
- iOS-aware file export — uses the native Share Sheet on iPhone where
  browser downloads are often blocked, falling back gracefully
- Built for real-world use on a small business's actual hardware and
  network conditions, not just a demo environment


A REAL DEBUGGING STORY
--------------------------
After deployment, the app started taking over a minute to load. Rather
than guessing, I used Chrome DevTools' Network tab to trace the issue
to a specific failing request — Firestore's real-time connection was
being aborted (NS_BINDING_ABORTED) by something on the network path,
forcing slow fallback retries. I diagnosed this directly from request
logs rather than assuming it was a code bug, ruled out the app code and
the Firebase project itself as causes, and isolated it to a connection-
type issue. This is the kind of root-cause network debugging that
doesn't show up in a typical tutorial project.


HOW IT WORKS (HIGH LEVEL)
-----------------------------
- All inventory items live in a single Firestore document, which every
  connected device subscribes to in real time
- Any change (quantity adjustment, add, edit, delete) writes back to
  that document, and Firestore pushes the update to every other open
  device instantly — no manual refresh needed
- The app seeds a small starter list only on a completely empty
  database; after that, all data is live and staff-managed entirely
  through the app's own UI


WHAT I'D BUILD NEXT
----------------------
- User accounts / role-based permissions (e.g. manager vs. staff)
- Historical tracking (usage trends over time, not just current stock)
- Push notifications for critical low-stock items
- Automated supplier email integration for the order list

================================================================
