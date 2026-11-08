# Test prompt injection with codewords

Prompt injection is invisible. A hook can report success, a log line can appear, and the model can still never receive the text. The cheapest reliable test is a codeword.

## The method

1. Put a unique, meaningless token inside the injected text. Example: `ZEBRA-42`.
2. Start a fresh agent instance with a trivial prompt.
3. Ask the model to repeat the token.

If the model returns the token, the text reached the model. If it does not, the injection path is broken. This works for system prompt injection and for tool-description augmentation. Use a different token per surface so you can tell which path carried it.

Run the test in a fresh process. A reused session may retain the token in its own history and produce a false pass.

## Do not trust substring probes

A probe once checked whether the injected system string contained `<delegation-policy>`. The actual string was `<delegation-policy priority="high">`. The probe returned false while injection was working perfectly. Hours went into investigating module identity and hook order before anyone checked the marker itself.

Exact-substring checks are brittle. Tags gain attributes, whitespace changes, and serializers reorder fields. Prefer a behavioral test that the model must satisfy. If you keep a structural check, parse the string instead of matching a literal.

## Test the negative path

Good tests cover more than the happy path:

- Remove the shared policy file. Confirm the inline fallback still injects.
- Change a marker in the file. Confirm the next run reads the new content.
- Run a child session. Confirm the policy is absent there.
- Disable the hook. Confirm the token is absent.

These four cases separate "the file exists" from "the system reads the file, scopes it, and falls back safely."

## Write assertions to a file

Inline one-liners in a shell are a trap. Quoting, interpolation, and escaping differ between shells, and a corrupted assertion looks like a failed feature. Put the assertion in a small script file, run it, and keep the output. The script is also the regression test for the next change.

## Log once, not per request

Hook logs are useful at load time: one line that says the hook is active and where its policy came from. Per-request logging floods the log and slows the hot path. Behavior tests are the evidence; logs are only orientation.

## A note on false confidence

A test suite that only checks that files exist will pass while the feature is dead. The test has to include the model. That is slower and less tidy, and it is the only version that answers the question you actually care about.
