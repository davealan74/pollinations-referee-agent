# pollinations-referee-agent

A Pollinations code agent that judges whether a "done" claim holds up against
its evidence (a diff, tool output, or test results), asking Jev
(`POST /alpha/decisions`) for a calibrated yes/no probability instead of
trusting the claim at face value.

Fork this repo, then create the code agent:

```bash
npx @pollinations/cli agents create --config code-agent.json
```

with `code-agent.json`:

```json
{ "type": "code_agent", "repository": "https://github.com/<you>/pollinations-referee-agent" }
```

Call it with `model: "<your-github-username>/referee"` on `/v1/chat/completions`
or `/v1/responses`, sending:

```json
{
  "input": "the null pointer bug is fixed",
  "metadata": {
    "evidence": "diff adds a null check before user.name; npm test passes 42/42",
    "threshold": 0.6
  }
}
```

Full write-up, tests, and worked examples:
[`apps/agent-referee/`](https://github.com/pollinations/pollinations/tree/main/apps/agent-referee)
in the main [pollinations/pollinations](https://github.com/pollinations/pollinations) repo.
