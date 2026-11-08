# Skill drift across harnesses

A skill is a file. A file copied into five places is five files. Without a canonical source, they drift, and the drift is silent.

## The failure mode

A skill was edited in two directories and reported as done. The user still saw the old content. A full-profile search found five copies:

- one in a canonical shared directory, read by two runtimes
- one in a runtime-specific directory, stale
- one in a third runtime's directory, stale
- one in a portfolio snapshot, stale by design
- one in a dated backup directory, dead

The edit had worked. The user was looking at a different copy. That is the normal shape of this bug.

## One canonical copy, then link

The durable fix is one source of truth plus links:

```
~/agents/skills/<name>/          # canonical
~/runtime-a/skills/<name>        # symlink or junction to canonical
~/runtime-b/skills/<name>        # symlink or junction to canonical
```

On Windows, a directory junction works without administrator rights. On Unix, a symlink works. The important property is that editing either path edits the same bytes.

Some runtimes do not follow links reliably, or resolve them differently under a sandbox. Verify with a real resolve of the skill file, not with a directory listing.

## Audit before you claim success

Before reporting a skill change:

1. Search the whole profile for the skill name.
2. Resolve every match to a real path.
3. Compare modification times and content hashes.
4. Identify which paths each runtime actually scans.

Runtime discovery paths are not obvious. Some read a shared directory, some read only their own. Read the installed package source or the runtime's own docs. Do not assume the path from a blog post.

## Separate live config from snapshots

A public portfolio copy and an archived backup are not live config. They will always be stale. Decide explicitly whether they should be updated:

- live skill directory: must match canonical
- portfolio snapshot: update on release, not on every edit
- backup directory: delete or date it; never treat it as a source

Mixing these categories causes the "I made the change but nothing happened" loop.

## Keep the skill self-contained

A skill that depends on a local path, a personal account, or a specific machine will break when copied. Write it so the procedure is portable: describe the intent, the required tools, and the failure modes. Put machine-specific paths in configuration, not in the skill body.

That also makes the skill safe to publish after a light sanitization pass.
