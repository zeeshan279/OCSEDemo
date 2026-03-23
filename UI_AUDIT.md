# UI Design Audit (March 23, 2026)

## Scope
Reviewed the following mock pages:
- `csp_contact_management_mock.html`
- `create_contact.html`
- `full_contact_details.html`
- `duplicate_review_merge.html`

## Key design issues

### 1) Form and filter placeholders are used as selectable values (High)
Several `<select>` controls present labels like "Application", "Status", and "Relationship Type" as ordinary options. This can make it unclear whether the field has a valid selection and can lead to accidental submission with placeholder-like values.

**Examples:**
- `create_contact.html` (`application`, `relationshipType`, `status`, `contactRole`)
- `csp_contact_management_mock.html` (`application`, `relationship-type`)

**Recommendation:** Use a disabled placeholder option (`value=""`, `disabled`, `selected`) and require a real user choice where needed.

### 2) Information hierarchy is weak in results/actions (Medium)
In Search and Duplicate Review, most action controls use the same visual weight (`usa-button--outline`), which reduces scannability and makes primary actions harder to identify quickly.

**Examples:**
- Search result row actions: "View Contact Details", "Mark Not Duplicate", "Compare Record"
- Duplicate review actions: both merge paths and "Mark as Not Duplicate" have near-equal emphasis

**Recommendation:** Keep one clear primary action per section (solid button), make secondary actions outline, and style destructive/irreversible actions distinctly.

### 3) Data formatting is inconsistent across pages (Medium)
Date formats vary between ISO (`2026-03-19`) and long format (`Mar 18, 2026`), which can reduce trust and force extra cognitive load.

**Examples:**
- `csp_contact_management_mock.html` metrics grid uses `YYYY-MM-DD`
- `full_contact_details.html` audit panel uses `Mon DD, YYYY`

**Recommendation:** Standardize date/time display format (e.g., `Mar 19, 2026`) and include timezone/time where operationally relevant.

### 4) Long-form details are dense and hard to scan (Medium)
The Full Details page places many similarly styled boxes together without section-level visual separation beyond headers.

**Recommendation:** Add stronger grouping cues (sub-card backgrounds, divider spacing, or iconography) and highlight critical values (status, primary contact method, latest update).

### 5) Search state feedback is minimal (Low)
Search results are simply hidden/shown; there is no explicit empty state, loading state, or status announcement beyond visibility changes.

**Recommendation:** Add dedicated states:
- Before search: guidance text
- Loading: progress indicator/skeleton
- No results: actionable empty state

## Quick wins (low effort)
1. Convert placeholder-like select options to disabled defaults.
2. Standardize button hierarchy in each panel to a single primary CTA.
3. Normalize dates to one display standard.
4. Add section spacing tokens to improve readability in `full_contact_details.html`.

## Overall assessment
The UI is structurally solid and uses USWDS components consistently, but it would benefit from stronger action hierarchy, more consistent data presentation, and improved search-state feedback to reduce user confusion during high-frequency workflows.
