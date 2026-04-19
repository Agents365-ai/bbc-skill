# Example: BV1NjA7zjEAU

Real output from running `bbc fetch BV1NjA7zjEAU` against a short educational
Bilibili video (UP主: 探索未至之境).

## What's in here

- `summary.json` — video metadata + aggregated stats + top-N comments (13 KB)
- `comments.jsonl` — 59 comments total (26 KB). One comment per line:
  - 44 top-level
  - 14 nested (楼中楼)
  - 1 pinned (UP置顶)

## Video at a glance (from summary.json)

- **Title**: 会魔法吗？3步搞定Claude Code、Google、Github、Hugging Face全通！
- **Duration**: 42 seconds
- **Stats**: 7,287 views · 97 likes · 70 coins · 116 favorites · 59 comments · 3 barrages
- **Tags**: 魔法, 学习, 教程, Google, 另类思路, Claude Code, Github, Gemini

## Suggested Claude Code prompts

### 1. Overview

```
Read examples/BV1NjA7zjEAU/summary.json and summarize:
- Who is the target audience (from title + tags + top liked comments)?
- What's the overall sentiment of comments?
- Which comments should the UP respond to that they haven't?
```

### 2. Keyword / theme extraction

```
Grep examples/BV1NjA7zjEAU/comments.jsonl for the 10 most common
meaningful phrases in `message` fields. Exclude stop words
(的/了/是/我/你/他/她) and single characters.
```

### 3. UP interaction audit

```
From examples/BV1NjA7zjEAU/comments.jsonl, list:
- Top-level comments with rcount > 0 that the UP (mid=441831884) did NOT
  reply to
- UP replies grouped by thread — were any threads neglected?
```

### 4. Geographic insight

```
Read summary.json ip_distribution. Which provinces are overrepresented
compared to typical Bilibili demographics? Any actionable takeaway for
the UP's content strategy?
```

### 5. Temporal pattern

```
Read summary.json time_distribution.by_day. Did the video have a
long tail of comments, or did engagement die off within 48 hours?
```

## Re-creating this example

```bash
./scripts/bbc fetch BV1NjA7zjEAU \
  --cookie-file ~/Downloads/bilibili_cookies.txt \
  --output ./examples/BV1NjA7zjEAU
```

Note: actual comment content may change if new comments are added or old
ones deleted. The snapshot here is from 2026-04-19.
