---
name: tailwind-color-arbitrary
description: Replace Tailwind CSS color-token classes with equivalent literal arbitrary-value classes, verify UI appearance, and remove unused color tokens only after explicit user approval.
---

# Tailwind Color Arbitrary

Migrate Tailwind color-token classes to literal arbitrary-value classes while preserving rendered UI. Adapt paths, file extensions, commands, and syntax to the target project. Do not assume a framework, Tailwind version, source layout, or package manager.

## 1. Inspect the project

1. Read project instructions and identify the framework, Tailwind version, CSS entry points, source directories, build setup, test conventions, and available validation commands.
2. Find CSS files that define Tailwind color tokens. Inspect the actual declarations and how the project's Tailwind version exposes them (for example, `@theme` variables or configuration files). Include custom color tokens only; do not mistake unrelated CSS variables or built-in Tailwind palette entries for project-defined tokens.
3. Search active application source and templates for usages of those tokens. Include class strings in markup, framework components, conditional expressions, class composition helpers, and recognized dynamic constructions. Exclude dependencies, generated output, and static snapshots unless the user requests them.
4. Record exact token values and every discovered usage with file path and line number. Distinguish confirmed matches from dynamic or ambiguous cases; never infer a runtime-generated class without evidence.
5. Determine the exact equivalent literal arbitrary class supported by the installed Tailwind version. Preserve the color's meaning and all relevant variants, such as opacity, hover/focus state, responsive prefixes, and important modifiers. Use literal values, not CSS variables, in replacement classes. Handle escaping and arbitrary-value syntax according to the project's Tailwind version.

## 2. Build a complete migration proposal

Before editing any file, prepare and show the user a complete plan. Include:

1. **Color-token inventory:** each token name, exact resolved color value, declaration format, and defining CSS file/line. If a value depends on another variable or cannot be resolved exactly, mark it unresolved and do not propose a guessed literal.
2. **Usage locations:** every file and line where each token is used. List ambiguous/dynamic usages separately with the expression and why it cannot be counted or mapped exactly.
3. **Usage counts:** count each occurrence of a token class, grouped by token and in total. State counting rules. Do not count token declarations as class usages. If dynamic usages prevent an exact count, provide a confirmed count and identify the uncounted cases.
4. **Class replacements:** show each distinct original class and its proposed literal arbitrary replacement, preserving modifiers and context. Include occurrence count and relevant file locations. For conditional/dynamic classes, show the exact transformation or mark it unresolved.
5. **Important findings:** CSS-variable dependencies, opacity behavior, duplicate values, token aliases, unsupported syntax, excluded files, and any other issue affecting correctness.
6. **Removal plan:** list exact CSS token declarations proposed for removal, and state that removal happens only after migrated usages and verification pass.
7. **Verification plan:** list project-appropriate commands and visual comparison method. Explain if baseline screenshots, a browser, or a visual test are unavailable.

Then ask the user to confirm the specific proposal. Do not edit source or CSS, run automated rewrites, or remove tokens before explicit approval. If the user requests changes or rejects it, revise the proposal and ask for confirmation again. Approval covers only the presented scope; new findings that change mappings, files, or risk require an updated proposal and renewed confirmation.

If no token usages are found, report the inventory and counts and ask whether the user still wants unused token definitions removed. Do not remove them without explicit approval.

## 3. Apply approved replacements

1. Apply only approved replacements. Preserve class ordering where practical and retain every variant, opacity, state, responsive prefix, and unrelated class.
2. Use literal color values from the verified token definitions. Encode values using valid Tailwind arbitrary-value syntax; do not leave references to the token CSS variable.
3. Do not change unrelated styles or rewrite ambiguous dynamic code. If implementation reveals an unapproved usage or a mapping that differs from the proposal, stop before changing that case, report the discrepancy, and request approval for an updated plan.
4. Keep token declarations in place during initial migration. Do not delete them yet.

## 4. Verify UI equivalence and references

1. Search active files again for every migrated token class and inspect remaining matches. Resolve confirmed in-scope matches. Explain intentional exceptions and excluded/dynamic cases.
2. Run the project's available formatter, lint, type-check, tests, and production build as appropriate. Use documented scripts and the detected package manager; do not invent commands.
3. Compare before/after UI using the same routes, viewport sizes, states, and data where possible. Prefer existing screenshot or visual regression tooling. If unavailable, use browser inspection when available and report precisely what was and was not compared. A passing build alone does not prove visual equivalence.
4. Review the diff for changed class semantics, arbitrary-value parsing/build output, opacity behavior, responsive/state variants, and unrelated edits.
5. If checks fail or visual differences appear, do not remove token declarations. Fix within approved scope or report the issue and ask how to proceed.

## 5. Remove approved color tokens

Only after migrated usages are verified and no in-scope dependency remains:

1. Recheck each proposed token declaration and its references across the repository, including CSS `var()` references and non-class usage. Color tokens may serve consumers beyond Tailwind classes.
2. If any remaining consumer exists, keep the relevant declaration and report it. Do not remove tokens still required by active code.
3. Remove only approved, unused color-token declarations. Preserve unrelated CSS rules and token declarations.
4. Rerun relevant search, build, and validation checks after removal. Compare UI again if token removal can affect runtime styling.

## 6. Report results

Summarize:

- tokens and class occurrences migrated;
- files changed and token declarations removed or retained, with reasons;
- unresolved/dynamic usages and intentional exceptions;
- commands run and their results;
- visual comparison method and outcome, including limitations;
- any remaining UI or verification concerns.
