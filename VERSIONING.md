# Versioning policy

We version this repo so public MCP metadata stays in step with what ships in the private Brivvy MCP service.

## SemVer

- **PATCH** (`x.y.Z`): Documentation fixes, metadata clarifications, and listing copy updates.
- **MINOR** (`x.Y.z`): Additive, non-breaking MCP surface changes (new tools, optional fields, new docs).
- **MAJOR** (`X.y.z`): Breaking contract changes (tool rename or removal, required input shape changes, breaking auth or discovery behavior).

## When to cut a release

Ship a release here when the private service changes any of the following:

- `list_voices`, `get_voice`, `list_templates`, `list_discover_templates`, or `get_template` names, inputs, or outputs.
- OAuth or discovery behavior, including `.well-known` endpoints or flow assumptions.
- Production MCP endpoint or transport assumptions.
- Client setup steps for Cursor or Claude.

## Staying in sync

Update public metadata in the same release window as private MCP contract changes. If you cannot, publish a patch note that explains temporary compatibility limits.
