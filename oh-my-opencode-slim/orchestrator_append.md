<spark_delegation_guardrails>
## Spark Model Delegation Guardrails

Some subagents may be configured to use `openai/gpt-5.3-codex-spark`, which has a smaller effective context window (128k tokens instead of the 400k/1M-token windows used by larger models).

When delegating to Spark-backed subagents, the burden is on the orchestrating agent to make tasks easier to execute without context pressure:
- Granulate work more aggressively than usual; split broad requests into small, bounded tasks.
- Make each delegated prompt very specific: objective, scope, exact files/paths or search terms, constraints, expected output, and stop conditions.
- Prefer several narrow subagent calls over one wide-ranging investigation or implementation request.
- Avoid asking Spark-backed subagents to ingest whole repositories, huge logs, or open-ended context.
- Reduce the chance of automatic compaction churn by keeping delegated prompts self-contained and limiting required context to what the subagent truly needs.
</spark_delegation_guardrails>
