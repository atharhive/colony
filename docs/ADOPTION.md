# Adoption

Independent work built on Colony, kept here because the submission asks whether anyone
else could run the thing.

## Atharium — jacksonjp0311-gif/atharium

Forked from `atharhive/colony` on 24 November 2026 by James Paul Jackson. Keeps the claim
map and puts a cyclic runner on top of it: on a schedule it measures the current knobs
against a fixed seed set, proposes one mutation from a closed set, re-measures, and keeps
the change only when the trial is strictly better, a frozen twin control does not lead,
and an oracle gate does not kill it. Human authorization is required for durable accepts.

What they kept from Colony, in their own files: `colony/cluster.py`, `colony/intents.py`,
`colony/verifier.py` — the cluster map, the claim registry, and the independent verifier.

What they added: `evolve.py`, `knobs.py`, `measure.py`, `oracle.py`, and a GitHub Actions
workflow that runs the loop on a schedule.

What that says about the boundary: the verifier was copied and left outside the mutation
set, which is the correct reading of the design. The parts that can change are the parts
that were new to them.

### Two things worth raising with them

1. **Overfitting.** A fixed seed set plus a gate that keeps anything strictly better is an
   optimization target. Without held-out seeds, the loop improves its score on those
   seeds rather than on the question. Worth asking whether accept-time scoring uses seeds
   the loop never sees.
2. **Test coverage of the moving parts.** They inherited the trust boundary and wrote
   `tests/test_verifier.py` against it. `evolve`, `knobs`, `measure` and `oracle` have no
   tests: the thing that cannot change is pinned, the thing that does change is not.

Both are the kind of notes a fork deserves: specific, arguable, and not a complaint about
credit.

### Why it is in this repository

The growth criterion for Season II asks whether an independent developer tried the work.
This is stronger than a try: someone read the geometry, agreed with it, forked it, and
built something on top that Colony itself does not do. The link is kept here so the claim
is checkable rather than asserted.
