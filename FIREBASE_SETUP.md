# Hallpass Buddy — Firebase setup

Firebase project ID: `hallpass-buddy`

## Before using student data
Confirm district approval for Firebase and student information. Keep using fictional names until approval, authenticated access, and Firestore rules have been tested.

## Firebase Console checklist
1. Firebase Console → Build → Authentication → Sign-in method → enable **Google**.
2. Authentication → Settings → Authorized domains → add your exact GitHub Pages hostname (`mnickelson-tech.github.io`), if not already present.
3. Build → Firestore Database → Create database → **Production mode**. Select a district-approved US region.
4. **Do not switch Firestore to test mode** or publish permissive rules.
5. Before production, deploy server-enforced rules that require a verified `@conroeisd.net` identity and limit writes to the signed-in teacher. A domain alone does **not** distinguish staff from students who may use the same domain.

## Planned data model
- `classrooms/{uid}`: teacher UID, display name, grade, room
- `passes/{passId}`: classroom UID, student display name, destination, status, timestamps
- `bathroomSlots/{uid}`: at most one active bathroom pass per teacher

Use Firestore transactions to claim/release a bathroom slot atomically. Firestore security rules must independently enforce ownership and valid transitions; client-side checks alone are insufficient.

## Current status
This is a configuration and implementation plan only. The existing `index.html` still uses browser `localStorage`; **the live database is not yet connected**.
