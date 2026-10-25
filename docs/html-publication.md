# HTML publication boundary

This is a sanitized instructions repository. It does not include the private HTML schemas, renderers, templates or execution evidence. Its application-writing workflow is not a replacement for the HTML research workflow.

## Authorized maintainer flow

In the private Application Writer Multi-Agent checkout, follow its workflow and retain the actual intermediate records privately. Its `scripts/writer_pipeline.py` provides `init`, `prepare`, `verify-prepare` and `publish-plan`. Use the private README and `docs/writer-pipeline.md` for the input contract and arguments; these paths refer to that checkout, not this repository.

Preparation validates stage records, source snapshots, revisions and the original report contracts. It renders with the original writer and merges allowed HTML/font assets into a separate public staging copy of the publication site. Existing reports, encrypted assets and unrelated files are preserved. Unknown markup or conflicting files fail instead of being overwritten.

Review the staged content and exact changed paths, then separately approve promotion, commit and push to the publication site. There is no background sync, automatic push or server-side gate added by this change. Hash checks establish byte identity and structural completeness; they do not establish factual truth or prove that an agent read a source.

## Public boundary

Do not export source JSON, source transcripts, research logs, private strategy, real execution records, personal career details, credentials or original private Git history. Existing encrypted publication assets must remain encrypted. Public reports themselves still require a disclosure review: file extensions cannot determine whether prose contains personal information.

This update only documents the connection and its boundaries. The private writer's synthetic validation and staging tests do not prove a complete application-writing, external-storage or form-submission run in this public edition. No missing renderer dependency has been replaced with a fallback here.
