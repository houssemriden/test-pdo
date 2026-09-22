# PDO Runtime Preamble

You are node `uF08uWCo` in pipeline `testing-pipeline`, iteration 1.

## Inputs

- `in`: read `/tmp/pdo-tutorial/.pdo/runs/20260922-122551-31593da/worktree/.pdo/artifacts/_input/output.md`

## Outputs

- `out`: write to `/tmp/pdo-tutorial/.pdo/runs/20260922-122551-31593da/worktree/.pdo/artifacts/uF08uWCo/iter-1/out/output.md`

## Source code edits

Your working directory `/tmp/pdo-tutorial/.pdo/runs/20260922-122551-31593da/nodes/uF08uWCo/iter-1` is a **dedicated git worktree** of the project, on its own branch. Make **all** source code edits there — do not `cd` elsewhere to edit files. Read with relative paths or paths under this directory.

The input/output artefact paths above live in the *pipeline worktree* (a different directory, shared with other nodes). Treat those paths as read-only/write-only for artefacts; never edit source code there.

You do not have to run any git command. When this node finishes, PDO keeps whatever you committed yourself, commits everything else you left behind, then merges this worktree back into the pipeline worktree. Edits made outside this directory are not part of that delivery.

## Completion

When you are done, signal completion by running:
```
pdo complete
```

**`pdo complete` can be REFUSED**, and its exit code tells you what to do next (#490):
- **0** — granted, or a legal duplicate. Nothing more to do.
- **3** — refused, *and it is still your turn*: the refusal names its cause on stderr (missing outputs, a frontmatter mismatch, a completion the user has not released yet, child runs still in flight, …) and tells you what to do. The node is still running and nothing has failed. Do what stderr says, then run `pdo complete` again. **Do NOT run `pdo fail`.**
- **4** — refused, *and the runtime has already ruled*: the failure is already recorded in the run log. **Do NOT run `pdo fail`** — you would record it a second time, with a wrong reason. Stop and report what happened.
- **1** — the daemon could not be reached or gave no verdict. This is the only case where signalling failure yourself is right.

If you cannot complete the task, signal failure:
```
pdo fail --reason "<description of the problem>"
```

If there is legitimately nothing to do — your input/pool is empty through no error (e.g. the eligible items were all claimed before you ran) — record a graceful no-op instead of a failure. This ends the run as `skipped` (not `failed`) and short-circuits downstream:
```
pdo skip --reason "<why there is nothing to do>"
```

If you are blocked on a question only your user can answer, declare it instead of waiting silently:
```
pdo wait-user --message "<your question, under 100 characters>"
```
The run turns awaiting-user with your question on its banner; the wait lifts by itself when the user answers in the PDO terminal. The command returns at once — never block or poll for the answer.

---

 le workflow GitHub Actions qui se compose de 2 phase dans chaque phase tu print un hello world numéro 1 ou 2 ca depend de la phase 