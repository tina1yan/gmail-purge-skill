# Gmail Purge Skill

A reusable agent skill for Gmail cleanup, unwanted mailing-list unsubscribe, label maintenance, and automatic classification audits.

**Status: instruction-based skill.** It works through the Gmail tools or browser/API capabilities available to your agent. It does not contain credentials, run a background service, install Gmail filters automatically, or delete mail merely because it is installed.

## What it handles

- Recover earlier cleanup decisions and preserve existing labels.
- Audit label coverage across recent and historical mail.
- Separate job alerts, applications, rejections, medical messages, financial records, receipts and newsletters.
- Backfill labels, archive authorized clutter, and move authorized unwanted mail to recoverable Trash.
- Unsubscribe from unwanted lists with a recorded outcome.
- Inspect existing incoming-mail filters, test criteria against counterexamples, and verify saved changes.
- Report actual counts, partial failures and capabilities that remain unavailable.

## Install

Copy `skills/gmail-purge` into your agent's skills directory. For Codex, the usual destination is `~/.codex/skills/gmail-purge`. Reload the skills list or start a new session if needed.

The skill folder includes `SKILL.md`, `agents/openai.yaml`, and two progressively loaded references. It does not depend on a particular connector's tool names or account identifiers.

## Example prompts

```text
Use $gmail-purge to audit my Gmail labels and incoming filters. Explain gaps and fix authorized labeling issues.

Use $gmail-purge to clean unwanted retail newsletters, unsubscribe from the selected lists, and preserve receipts, work correspondence and account alerts.

Use $gmail-purge to reconcile the existing Job Alerts and Job Applications labels. Check that interview invitations are never hidden by a rejection rule.
```

## 中文说明

这是一个整理 Gmail 的可复用 skill：清理历史邮件、退订不想要的订阅、补齐分类标签，以及核对未来邮件的自动过滤规则。

它区分三件事：**给历史邮件打标签、真正发出退订请求、保存未来自动分类规则**。完成其中一项，不能说另外两项也完成了。

保留已有标签体系；优先保护医疗预约、账单收据、求职回复、工作沟通和账号安全通知。促销分类里也可能有重要邮件，因此不会仅凭 Promotions、未读或邮件年代就批量删除。`purge` 这个名字不代表授权清空邮箱。

如果 Gmail 工具只能读写邮件、不能读取过滤器，skill 会继续完成可执行的部分，并明确标记过滤器尚未更新。安装这个 skill 本身不会创建定时任务或后台自动化。

## Privacy and validation

This public repository contains reusable instructions and fictional examples only. Real mailbox inventories, email content, addresses, message IDs, raw headers, unsubscribe links and filter exports belong in a separate private workspace.

The skill was structurally validated with Codex's skill validator and reviewed against Gmail's official filter/subscription documentation and RFC 8058. No claim is made that all connector implementations, unsubscribe providers or future-delivery behavior have been tested. See the references inside the skill for verification steps and source links.

## License

[MIT](LICENSE)
