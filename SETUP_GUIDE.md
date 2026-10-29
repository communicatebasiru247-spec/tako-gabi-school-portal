# Tako Gabi School Portal — setup guide

## Important
This is a starter, not an audited production school system. Test with fictional records first. Do not upload real student data until rules, backups, privacy notices, account recovery and local requirements have been reviewed. Never put service-account credentials in HTML. Firebase web config is not a password; Firestore Security Rules protect records.

## 1. Create Firebase
1. Visit https://console.firebase.google.com/ and create a project.
2. Open Build → Authentication → Get started → Sign-in method; enable Email/Password.
3. Open Build → Firestore Database → Create database. Choose a region carefully.
4. Project settings (gear) → General → Your apps → Add app → Web. Register the website and copy the `firebaseConfig` values.
5. Open `index.html` in Pydroid 3 and replace the `PASTE_..._HERE` values in `firebaseConfig` with the real values from Firebase. Keep quotes and commas.

## 2. Publish Firestore rules
1. Firebase Console → Firestore Database → Rules.
2. Copy all of `firestore.rules` into the editor and click Publish.
3. Test with separate accounts/roles before entering real data. Public admission enquiries need abuse prevention (App Check, validation/rate limiting through a trusted backend) before a public launch.

## 3. Run / edit in Pydroid 3
1. Extract the ZIP and open `index.html` in Pydroid 3 to edit it.
2. Internet is needed for Firebase scripts and online data.
3. Some browsers restrict Firebase authentication from a local `file://` address. If local login fails, deploy to HTTPS and test the hosted website.

## 4. Free hosting with GitHub Pages
1. Create an account at https://github.com/ and a new public repository, e.g. `tako-gabi-school-portal`.
2. Upload `index.html` to the repository root. Do not upload real student data, passwords or private keys.
3. Repository Settings → Pages → deploy from a branch → `main` → `/ (root)` → Save.
4. Wait for GitHub Pages to show the HTTPS site URL.
5. Firebase Console → Authentication → Settings → Authorized domains: add the hostname from your GitHub Pages URL (usually `yourname.github.io`).
6. Open the HTTPS site and test account registration/login. Firebase Hosting is another option, but CLI deployment usually needs a terminal or supported cloud development environment.

## 5. Create the first admin account
1. Open the hosted site and use Request an account to create your own account.
2. Firebase Console → Authentication → Users: copy your account UID.
3. Firestore → Data: create collection `users`, then a document whose ID is exactly that UID.
4. Add fields: `name` (string), `email` (lowercase string), `role` (string `admin`), `studentId` (empty string), `linkedStudentIds` (empty array), `assignedClasses` (empty array).
5. Sign out and back in. Never give admin role to untrusted accounts.

## 6. Set up other accounts (admin does this manually)
All role assignment/linking must be done in Firestore by a trusted admin after checking identity.
- Teacher profile: `role: "teacher"` and `assignedClasses: ["Primary 4","JSS 1"]` (class names must match exactly).
- Student profile: `role: "student"` and `studentId: "ADM001"` matching the student document ID.
- Parent profile: `role: "parent"` and `linkedStudentIds: ["ADM001","ADM002"]` for verified children.
- Include `name`, `email`, `studentId`, `linkedStudentIds`, and `assignedClasses` fields in each user profile. Use empty string/arrays when not applicable.

## 7. First-use workflow
1. Admin adds classes using consistent names (e.g. Nursery 1, Primary 1, JSS 1, SSS 1).
2. Admin adds students using unique admission numbers; IDs are saved uppercase.
3. Students/parents/teachers request accounts. Admin verifies them and sets roles/linkages in Firestore.
4. Teachers submit unpublished results; admin can add a result with published status from the admin portal. The starter does not yet include a polished review/publish screen.
5. Admin publishes announcements.

## Collections
`users`, `students`, `classes`, `results`, `announcements`, `admissions`.

## Before real school use
This starter has no attendance, fee payments, timetable, report-card PDF, bulk import, password reset screen, audit logs or result review/publish interface. Parent/student linking is manual. Public admission form needs anti-abuse protection and a privacy notice. Firestore may request an index; follow its console link. Test that students/parents cannot see unrelated or unpublished results. Check Firebase quotas/pricing in Console; free quotas can change.
