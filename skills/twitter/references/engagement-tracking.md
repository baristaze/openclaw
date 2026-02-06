# Engagement Tracking

This skill must never engage with the same tweet more than once.

## Canonical Identifier
A tweet is uniquely identified by:
- tweet_id if visible
- otherwise full tweet URL

## Storage
All engagements must be recorded in:
`~/.openclaw/twitter/engagement-log.csv`

Create the directory and file if they don't exist.

## Workflow Rule
Before any reply, quote, or interaction:
1. Check the engagement log
2. If tweet_id or tweet_url already exists:
   - skip the tweet
   - continue discovery

After a successful engagement:
- append a new row with:
  - tweet_id
  - tweet_url
  - engagement_type (reply | quote | original-reference)
  - timestamp
  - optional notes

## Failure Handling
If the log cannot be read:
- assume conservative behavior
- skip engagement rather than risk duplication
