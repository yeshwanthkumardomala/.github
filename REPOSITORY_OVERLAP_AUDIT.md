# Repository Overlap Audit

**Scope:** Read-only comparison of inventory and attendance repositories. This report is on the `audit/repository-overlap-review` branch; no project repositories were merged, deleted, renamed, archived, or modified.

## Inventory projects

### `YIMS`
- Modern TypeScript/React application with a substantial component tree, admin tooling, Electron entry point, and Supabase-related configuration.
- README advertises a live demo: https://yims.yesh5.in/
- Best candidate to present as the modern, hosted/showcase YIMS project, pending runtime/security checks.

### `YIMS-1`
- Separate Node.js/Express + SQLite application with backend routes for auth, items, locations, scanner, stock, usage, labels, and CSV.
- README describes an offline-first local-network inventory system.
- This is not simply a duplicate copy of the current `YIMS`; it has a distinct architecture and offline/LAN use case.
- Recommendation: retain as the local/offline edition or legacy implementation, and state that distinction in both READMEs if it is intentional.

### `Campus-Inventory-IMS`
- Lightweight HTML/JavaScript frontend backed by Google Sheets and Apps Script; supports QR scanning, inventory, and transactions.
- Its deployment notes include a public Apps Script deployment identifier and instructions indicating broad access. Review the Apps Script's authorization and write permissions before continuing to use it with real inventory.
- Recommendation: classify as an earlier campus-specific prototype or deployment, rather than another canonical YIMS, unless it is still the live system used in a lab.

### `yims-codex`
- Not accessible through the current GitHub API connection during this pass (404). This does not prove that it was deleted; it may be private, renamed, or unavailable to the connection.
- Recommendation: do not archive or remove it until its current status and contents are confirmed.

### Inventory decision
Do **not** merge or delete repositories yet. Tentative roles:
1. `YIMS` — modern/showcase edition.
2. `YIMS-1` — offline/local-network edition, if still useful; otherwise mark it as legacy after checking usage.
3. `Campus-Inventory-IMS` — campus-specific prototype/legacy deployment, unless it remains operational.
4. `yims-codex` — pending access/status confirmation.

**Security note:** `YIMS` has a tracked `.env` containing Vite/Supabase client configuration. A Supabase publishable/anon key is normally designed to be public, but it must be protected by correctly configured Row Level Security and policies. Confirm that no service-role key, database password, or other server secret is present in history. Prefer an ignored local `.env` plus a committed `.env.example` with placeholders.

## Attendance projects

### `student-attendence-jnv`
- Private web app built around a mobile-first hostel attendance workflow, with role-specific dashboards and Supabase integration.
- This appears to be the most complete web-oriented attendance product in the group.
- Keep private while it contains school-specific workflows or any real student/staff data. Verify database policies and avoid using real student records in development/demo environments.

### `JNVRR` (archived)
- Android/Kotlin project with attendance-related screens, including house, principal, and PT dashboards, plus a local database/repository/sync layer.
- Its README is generic AI Studio boilerplate rather than project documentation.
- This is a distinct native Android implementation, not necessarily a duplicate of the web app.
- Recommendation: keep archived if it is no longer maintained; update documentation only if you intentionally resume it. Do not unarchive merely to tidy the profile.

### `jnv-attendance`
- Not accessible through the current GitHub API connection during this pass (404). The previous metadata view described it as a prototype, but its current contents/status could not be verified.
- Recommendation: confirm whether it is empty, private, renamed, or deleted before taking action.

### Attendance decision
1. Treat `student-attendence-jnv` as the current web implementation **provisionally**, subject to checking deployment and real usage.
2. Keep `JNVRR` archived as the Android prototype/alternative unless you plan active development.
3. Leave `jnv-attendance` untouched until its status and contents can be confirmed.

## Reversible next steps
- Add explicit `Current`, `Prototype`, or `Archived/Legacy` wording to the relevant READMEs after confirming intended roles.
- Update the repository catalog to show one primary project per use case and link alternatives as prototypes/legacy versions.
- Before any archive/delete/merge operation, create a backup or tag and verify that no deployment, database, student data, or external integration depends on the repository.
- Review public deployment permissions and environment files before putting real data into either inventory or attendance systems.

This is a repository-structure and documentation audit, not a full code, dependency, or security audit.
