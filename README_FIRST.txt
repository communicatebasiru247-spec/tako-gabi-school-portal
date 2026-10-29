TAKO GABI SCHOOL PORTAL — FIREBASE CONNECTED STARTER

Files:
- index.html: responsive school portal with Firebase configuration included
- firestore.rules: Firestore security rules to publish/review
- SETUP_GUIDE.md: setup and deployment notes

Firebase project configured:
- Project ID: tako-gabi-school-portal
- Authentication providers: Email/Password and Google (as enabled by the owner)

IMPORTANT SAFETY NOTES:
1. This is a starter project and has not been security-audited or tested in your live Firebase project.
2. Do not enter real student records until you test rules and role permissions with test accounts.
3. Review/publish firestore.rules in Firestore > Rules only after understanding its access behavior.
4. Firebase web config is not a server secret, but security depends on Authentication, Firestore rules, and authorized domains.
5. Keep admin account credentials private. New user profiles are pending by default; role assignment must be done securely by school management.
6. Firebase backups and hosting may incur charges; check pricing before enabling paid services.
