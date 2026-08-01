# Changelog

## 0.2.0

- Correct the minimum supported runtime to Mog 0.1.4, the first release that
  embeds its configured package-compatibility version correctly.
- Add pinned CI/release automation with tag checks, 0.1.4/current-runtime tests,
  checksummed archives, and automated action updates.
- Add checked constructors, kind/null inspection, and typed accessors for every
  JSON value kind so the API contract describes supported DOM construction and
  reads without relying on fields that the current contract grammar cannot
  express.
- Reject non-finite numbers during construction and serialization.
- Replace module-global parser input and cursor state with state local to each
  parse call.
- Document installation, errors, duplicate-key behavior, compatibility, and the
  risks of directly mutating the public DOM.
- Expand tests for constructors, accessors, empty values, negative zero, and
  malformed inputs.
- Correct manifest license metadata to `GPL-3.0-only` to match `LICENSE`.

## 0.1.1

- Serialize JSON control characters with the required single escaped form.
- Document and require Mog runtime 0.1.1 or newer for JSON string processing.

## 0.1.0

- Initial foundation package contract.
