# Gmail filter audit and repair

Use this reference for incoming-mail rules, not merely historical label backfills.

## Inspect

Use Gmail Settings -> See all settings -> Filters and Blocked Addresses, or an existing authorized Gmail API client with the needed settings capability. Export or privately record rules before changing them. Do not request broader OAuth access merely to avoid an available supported route.

For each rule capture: current identity, exact sender/recipient/subject/query criteria, exclusions, target label, skip-inbox, mark-read, delete, forwarding and spam-related actions. Labels and filters are separate resources. Deleting a label is not a safe way to repair its filters.

## Decide whether an update is needed

| Observation | Interpretation | Next action |
| --- | --- | --- |
| Label exists but is empty | May be unused, new, too narrow, or have no matching mail | Search expected examples and inspect its rule |
| Recent expected mail lacks the label | Coverage gap is demonstrated | Compare sender variants and actual criteria |
| Some rejection mail is correctly filed | Does not prove an incoming filter caused it | Inspect saved rules; another automation/manual action may have labeled it |
| Entire ATS domain is archived | Interviews and verification mail may also match | Narrow to observed rejection content; preserve positive/actionable messages |
| Promotions include workplace or event instructions | Gmail category is too broad for deletion | Add sender/purpose safeguards; inspect cross-matches |
| Duplicate rules | Multiple actions may combine | Compare actions before removing an exact duplicate |
| Filter editor is unavailable | Future behavior cannot be confirmed | Complete authorized backfills, retain a private proposed diff |

## Test candidates

Use the intended account's Gmail search. Examples below are fictional patterns, not rules to install blindly:

```text
from:billing@example.com subject:"statement is ready"
from:alerts@example.com subject:"new jobs"
from:clinic@example.com
```

Examine representative positives and counterexamples: an interview invitation versus a rejection, a bank receipt versus a sale, an appointment reminder versus a wellness newsletter. Gmail search may match quoted material too, so an old rejection quoted in an active conversation is not sufficient evidence for automatic archiving.

For new rules, start with labeling only unless skip-inbox or mark-read is explicitly wanted and the criteria have been checked. Avoid depending on mutable mailbox state, such as an already-applied custom label, for an incoming filter. Do not assume Gmail provides first-match-wins rule ordering or that a protective rule cancels a delete action in another rule.

## Save and verify

- Compare against existing criteria/actions before creating a new rule. Gmail API filters expose create/list/get/delete operations; do not invent an update endpoint. If replacement is needed, keep a private record of the old rule and minimize the interval with overlapping actions.
- A new incoming rule and applying it to past messages are distinct operations. An importable XML file is a proposal until imported and read back in Gmail.
- Verify the exact saved criteria and actions. Re-read known positive and negative message examples after any historical backfill.
- Record `SAVED_RULE_VERIFIED` separately from `FUTURE_DELIVERY_VERIFIED`. The latter requires a newly received matching message; do not manufacture a test email or claim future delivery from historical mail.
- Do not silently add forwarding, whitelist all mail from a domain, or disable spam protection as a classification fix.

Official references:

- [Create, edit, export and import Gmail filters](https://support.google.com/mail/answer/6579?hl=en)
- [Gmail API filter settings](https://developers.google.com/workspace/gmail/api/guides/filter_settings)
- [Search differences between the Gmail API and UI](https://developers.google.com/workspace/gmail/api/guides/filtering)

Check current documentation when implementing an API adapter; this skill contains no Gmail credential client.
