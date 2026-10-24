---
name: draft-post
description: Write an X post and save it as a draft in Content Mill. Use when the user wants to draft, write, rework or save an X post without publishing it yet.
user-invocable: true
---

# /content-mill-x:draft-post

Saves an X post as a **draft**. A draft is never published; the user reviews it in Content Mill or asks you to publish it later with `/content-mill-x:publish-post`.

Arguments passed: `$ARGUMENTS` (the idea or text for the post; ask if it is empty).

## Steps

1. Call `list_social_accounts` and use only accounts whose status is Connected. If more than one X account is connected and it is unclear which the user means, ask.
2. Call `get_platform_limits` before writing so the text and media fit. An X post is at most 280 characters, with up to 4 images, or one GIF, or one video (never mixed); media is optional.
3. Media, if the user wants any: call `upload_media_from_url` with a public https link, or `create_media_upload` then `finish_media_upload` for a file that has no link. Never put file contents in a tool argument.
4. Write the post to fit, then call `create_draft` with `content`, `account_ids` and any `media_urls`. Give it a short `display_name` if it helps the user find it later (it is never sent to X).
5. Tell the user the draft was saved and what it says. To change it later use `update_draft`; say what will change first, because it overwrites the draft and keeps no earlier version.

Nothing in this skill publishes anything.
