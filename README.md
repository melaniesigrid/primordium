<div align="center">

# PRIMORDIUM

**A controlled, browser-native experiment in predator–prey coevolution — one that can come back null.**

Two species of neural network — one hunting, one fleeing — evolve against each other under the law of the Red Queen. Brains have evolvable topology, recurrence, and within-lifetime plasticity. None of it is designed; all of it emerges from mutation and selection.

*A reproduction in miniature, not a discovery. It runs entirely in your browser — no build step, no server, nothing sent anywhere.*

</div>

---

## The question

> Does predator–prey coevolution actually **cycle** — strategies chasing each other round in a loop, as the Red Queen predicts — or does the arms race grind to a stalemate?

Primordium doesn't assert an answer. It **tests** one, with a control, replicate runs, and a permutation test whose verdict is computed from the data — including "no effect."

## Run it

It's a single static HTML file with zero dependencies (Google Fonts are loaded from CDN; everything else is vanilla JS + Canvas).

```bash
# Easiest: just open the landing page
open index.html          # macOS
xdg-open index.html      # Linux

# Or serve locally (any static server works)
python3 -m http.server 8000
# then visit http://localhost:8000
```

- **`index.html`** — landing page: what this is and how it works.
- **`lab.html`** — the experiment itself (four interactive views).

## The three mechanisms (none of them designed)

| Mechanism | What it is | Emergence (10 runs) |
|---|---|---|
| **Recurrence / memory** | Connections that point backward or self-loop carry the previous step's activation forward, giving genuine internal state. | recurrence in **10/10** |
| **Lifetime learning** | Every synapse owns an evolvable learning rate `eta`; weights are nudged during an encounter by reward-modulated Hebbian plasticity. The *rule* is inherited, not the learned weights. | plastic synapses in **10/10** |
| **Evolvable topology** | NEAT-style structural mutation adds nodes and connections under a global innovation registry, with compatibility-distance speciation and explicit fitness sharing. | hidden nodes in **9/10** |

## How a generation turns

1. **Sense** — each agent reads the relative bearing, distance, and motion of its rival across a toroidal (wrap-around) arena.
2. **Encounter** — networks drive turn & thrust over a timed chase. The predator is slightly faster, the prey slightly more agile. Payoff is continuous and zero-sum, so there's always a selection gradient and no saturating ceiling.
3. **Compete** — every individual is scored against a *random sample of the opposing population* over several encounters with randomized geometry, to discourage overfitting to one opponent.
4. **Select** — fitness-shared selection, then mutation of weights, learning rates, and topology. The next generation enters the arena.

No training data, no gradient descent, no objective beyond "close the distance" (predator) / "open it" (prey).

## The experiment

- **H1** — under live coevolution, the prey's evasion-alignment trait *oscillates* (cyclicity) more than under a control where prey adapt to a **frozen** predator panel.
- **H0** — no difference: coevolution yields no more cycling than directed convergence.
- **Statistic** — depth of the deepest negative auto-correlation trough of the detrended trait series (lags 1–10).
- **Test** — two-sided permutation test, 20,000 shuffles, decided before running.

A second lens, the **CIAO matrix**, pits every predator generation against every prey generation. Non-monotone bands — a newer predator *losing* to an older prey — are the direct fingerprint of intransitive, Red-Queen dynamics. The two lenses can disagree, and that disagreement is itself informative.

## The four views

| Tab | What you do |
|---|---|
| **Arena** | Pit an evolved predator from one generation against prey from another; lock to the diagonal or break it to expose the Red Queen directly. |
| **Laboratory** | Run the pre-registered test: coevolution vs frozen-target control, replicates, permutation p-value, CIAO matrix. |
| **Brain** | Inspect an actual evolved genome drawn live — excitatory/inhibitory edges, dashed recurrent loops, ringed plastic synapses, brightness tracking activation. |
| **Monograph** | A short field write-up of the methods, the two measurement lenses, and an honest account of what this is *not*. |

## What this is not

It is **not a novel result.** Cliff & Miller coevolved recurrent pursuit/evasion networks and built CIAO plots three decades ago; this reproduces that lineage in miniature. Population sizes, mutation rates, and arena constants are hand-tuned for tractability in a browser, not derived. With a handful of replicates the permutation p-value is noisy — treat a single run as suggestive, not decisive, and raise the replicate count to tighten it.

Coevolution frequently fails to produce clean cycling, collapsing instead into disengagement or "mediocre stable states." **A null here is a real outcome, not a failure of the instrument**, and the code does not tune itself toward significance.

## Lineage of the methods

- Van Valen, L. **A New Evolutionary Law.** *Evolutionary Theory* 1: 1–30, 1973. *(The Red Queen.)*
- Cliff, D. & Miller, G. F. **Tracking the Red Queen.** *ECAL* 1995, 200–218. *(CIAO plots; coevolved recurrent pursuit/evasion nets.)*
- Stanley, K. O. & Miikkulainen, R. **Evolving Neural Networks through Augmenting Topologies (NEAT).** *Evolutionary Computation* 10(2): 99–127, 2002.
- Soltoggio, A. et al. **Evolutionary Advantages of Neuromodulated Plasticity.** *ALIFE XI*, 2008. *(See also "Born to Learn," Neural Networks, 2018.)*
- Ficici, S. G. & Pollack, J. B. **Challenges in Coevolutionary Learning.** *Artificial Life VI*, 1998. *(Mediocre stable states.)*
- Yaeger, L. **PolyWorld: Life in a New Context.** *Artificial Life III*, 1994. *(The spiritual ancestor.)*

## License

MIT — see [LICENSE](LICENSE).
