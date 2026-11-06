---
name: gmail-purge
description: Audit and clean a Gmail mailbox, unsubscribe from unwanted mailing lists, reconcile labels, and maintain incoming-mail filters while preserving important correspondence and verifying each change.
---

# Gmail Purge

Turn an overflowing mailbox into an inspectable filing system. Treat historical cleanup, unsubscribe requests, and future automatic classification as separate operations with separate evidence. A label alone is not a filter, and a skill installation is not a running automation.

## Establish scope and recover context

1. Resolve the intended Gmail account from the user's request and connected profiles. Never infer the account from a numeric browser URL. Ask only when multiple accounts remain plausible for a write.
2. If the user refers to earlier work, find the relevant conversation, private maintenance record, and current settings. Preserve exact existing label names. Record inaccessible/truncated history as incomplete; do not reconstruct old rules from memory as if verified.
3. Distinguish an audit request from authorization to label, archive, Trash, unsubscribe, or change filters. Follow existing explicit authorization without repeating permission requests. Broad cleanup does not mean permanently emptying the account.
4. Prefer connected tools. Inspect their current schemas: account identifiers, pagination, message versus thread behavior, and supported mutations vary. If settings or subscriptions are unavailable, use an authorized browser/API if available; otherwise finish independent work and report the exact remaining capability gap.

## Audit before changing

- List labels with message and thread totals. Use message counts consistently for before/after comparisons; categories and user labels overlap and must not be summed as a mailbox total.
- Inspect existing filters separately, including their criteria, actions and blocked senders. If filters cannot be read, their status is **NOT VERIFIED** even if recently received mail has labels.
- Search recent mail, archived mail, and older date slices. Use a bounded metadata sample first; read plain-text or HTML MIME bodies when sender/subject/snippet is insufficient. Do not fetch unrelated attachments or save verification codes.
- Find empty, overlapping or obsolete labels; unlabelled relevant messages; new sender variants; and messages affected by conflicting rules. An empty label is evidence to investigate, not proof of a broken filter.
- Inspect Spam separately for obvious false positives. Do not open links in suspected phishing messages. Do not treat every promotion, old message, unread message or mailing list as junk.
- Preview each proposed search and test counterexamples before applying it across history. State sampled coverage honestly; a page of 100 results is not the entire mailbox.

## Classify with useful distinctions

Reuse the user's taxonomy. These are optional examples, not a fixed schema:

| Mail purpose | Example label | Default handling when unclear |
| --- | --- | --- |
| Personal and active work correspondence | Existing work/personal label | Keep visible |
| Applications, interviews and recruiter replies | Job Applications | Keep visible; separate from job ads |
| Confirmed rejection or closed hiring process | Job Rejections | Read content before classification |
| Automated job recommendations | Job Alerts | Label; archive only within authorized scope |
| Appointments and medical correspondence | Medical | Preserve visibility and unread state |
| Statements, taxes, insurance and legal records | Finance & Legal | Preserve; distinguish marketing from transactions |
| Purchases, invoices and shipping | Receipts & Orders | Preserve records and active delivery notices |
| Account access and security notices | Existing security label if useful | Keep visible; never unsubscribe as promotions |
| Chosen newsletters and retail promotions | Promotions & Newsletters | Label; respect keep-list preferences |
| Ambiguous unwanted subscriptions | Review - Unsubscribe | Candidate only; not evidence of unsubscribe |

An interview reminder and a rejection can come from the same ATS address. A bank can send both statements and offers. Workplace notices and event check-in instructions can appear in Gmail's Promotions category. Prefer exact senders plus purpose-specific criteria to broad domains or ambiguous words such as `application`, `unsubscribe`, or `thank you`.

## Execute historical cleanup

1. Build a private change manifest containing the account alias, timestamp, operation, exact query or message IDs, original labels for enumerated messages, proposed changes and rollback method. Do not commit it to a public repository.
2. Start with additive labels. Avoid unnecessary duplicate labels. Preserve INBOX and UNREAD unless changing them is within scope.
3. Use server-side bulk labeling for vetted queries when supported. Record matched counts as matched, not newly labeled. For client-side batching, gather and deduplicate message IDs before modifying the result set; pagination over a changing search can skip messages.
4. For mixed conversations, mutate individual messages unless every message in the thread has been reviewed for the requested thread action. Archiving a thread may hide important replies as well as the promotional message.
5. Archive confirmed low-value mail when authorized. Move confirmed unwanted mail to recoverable Trash when deletion is authorized. Permanent deletion or emptying Trash requires specific authorization and any applicable action-time confirmation. Never equate the word “purge” with permission to erase all mail.
6. After a timeout, read back affected state before retrying. Reapplying a label can be idempotent; sending another unsubscribe email or recreating a filter may not be.
7. Verify labels on sampled message IDs, query for remaining misses, and read label totals again. Preserve evidence of partial failures; do not report success from an attempted call alone.

## Stop unwanted subscriptions

Read [references/unsubscribe.md](references/unsubscribe.md) before performing unsubscribe actions. Separate desired newsletters from unwanted promotions, and maintain a private keep-list when the user has supplied preferences. Do not turn a marketing unsubscribe into a paid subscription cancellation or account deletion.

## Repair future automatic classification

Read [references/filter-audit.md](references/filter-audit.md) when reviewing or changing filters. Preview the exact criteria, preserve existing rules, reconcile duplicates and conflicts, then verify the saved rule. If only historical labeling was possible, explicitly state **FILTERS NOT UPDATED**. Never claim that a newly created label will automatically classify future mail.

## Finish with evidence

Report the affected account alias, audited time range, before/after label counts, actual mutations, unsubscribe statuses, saved-filter verification, and remaining gaps. Distinguish changed-message totals, matched-message totals and overlapping label applications. Do not describe sampled work as a complete mailbox purge.

Keep real email bodies, sender inventories, account addresses, message/thread IDs, raw headers, filter exports, unsubscribe tokens and private chat excerpts outside the public skill. Use fictional `example.com` data for documentation. If asked to publish, publish only the reusable method and validate the public file list before pushing.
