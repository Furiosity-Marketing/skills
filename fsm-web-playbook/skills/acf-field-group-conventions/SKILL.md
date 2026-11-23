---
name: acf-field-group-conventions
description: >-
  Designs and revises Advanced Custom Fields (ACF) field groups for WordPress.
  Use when building or changing a post type's editor, mapping a page design to
  ACF fields, or reviewing field order, labels, defaults, tabs, and validation.
---

# ACF Field Group Conventions

Build the editor in the order a Furiosity Marketing content editor will enter
the page. Follow the target site's existing conventions and explicit requirements
where they differ from these defaults.

## Map the editor before building

1. Read the page design, template, and supplied copy. Walk one real entry through
   the proposed editor from top to bottom; use the copy's order to check the design.
2. Map each section to its editor label, editable heading default (if any),
   content fields, and what is required to publish. Flag discrepancies between
   the copy and template rather than guessing at the section order or required fields.
3. Inspect the existing field group, saved content, and template consumers before
   changing a field. Determine whether the site uses ACF Local JSON, PHP registration,
   or database-managed groups; edit the site's existing source of truth.

## Lay out the form for content entry

- Prefer one top-to-bottom form. Keep related fields together under clear section
  headings and put shared metadata next to the content that uses it. Keep tabs
  few and reserve them for distinct workflows, not each page section.
- Put secondary controls such as card/promotion settings and internal fields at
  the end, collapsed when supported. Keep routinely edited fields visible.
- Name sections for the editor's task, not for the public copy. For example,
  label the section **The Problem**, but prefill its editable **Heading** with
  **What We Heard**. Likewise, **The Solution** can default to **What We Did**,
  and **Project Showcase** to **See The Work**.
- Use ACF's `default_value` for approved editable copy on field types that support
  it. Don't use a placeholder, “leave blank for default” instructions, or only a
  template fallback. Leave fields without approved defaults blank. Don't overwrite
  saved values or treat a new default as a backfill for existing entries.
- Preserve existing group keys, field keys, field names, and stored layout names
  when relabeling or reordering. If the storage shape must change, plan the data
  migration and verify existing entries still load and render.

## Validate at publish time

- Keep new entries, draft saves, and autosaves free of missing-content warnings.
  Don't set ACF's **Required** flag for a publish-only requirement if it blocks
  draft saves in that editor.
- Validate publish requirements server-side on publish and schedule attempts,
  and on updates that must satisfy the same published-content rules. Check
  conditional fields only where applicable; for instance, don't require an end
  date for an ongoing project. Follow the site's policy for legacy entries.
- On an invalid attempt, name the missing fields and where to fix them in one
  short checklist. Block only actual publication requirements; keep advisory
  warnings non-blocking. Don't show the checklist on initial load of a blank draft.

## Check on staging

- Open a new entry and check the order, labels, and prefilled headings. Edit a
  heading, save a partial draft, and reload to confirm the edit persists without warnings.
- Try to publish and schedule with a required value missing. Confirm the check
  runs at the right time, then complete the required fields and confirm both
  paths work. Leave optional fields empty in the test.
- If the same rules apply to published edits, clear a required value on a
  published staging entry and try to update it. Confirm the update is rejected
  with a useful message and the previous published value stays intact.
- Reopen an existing entry and preview the rendered page. Confirm stored values
  and overrides survived and approved headings appear as expected.
- If using Local JSON, commit the updated definitions. Follow the repo's sync
  rules; update an existing database group in place rather than importing a
  duplicate with the same key.
