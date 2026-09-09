# Interactive toy: adversarial IRL with and without success feedback

Anonymous supplementary material for a paper under review. Open
[`index.html`](index.html) — or the hosted page — and play with it; nothing to build,
no dependencies, no network calls except a web font.

## What it shows

A minimal inverse-RL game in the plane. A ground-truth distribution of good behaviour
supplies a handful of demonstrations; the policy is a Gaussian whose mean you watch move;
a small tanh critic is trained to score demonstrations above the policy's own samples, and
the policy climbs whatever reward that produces. Both keep training, each responding to the
other, as in a GAN.

**Success feedback** changes exactly one thing: policy samples an operator labels successful
are dropped from the critic's negative batch. The questions appear one at a time, each asking
something you can then test with a slider:

1. the feedback toggle — is the policy allowed to stay once it reaches the demonstrations?
2. placing the policy by hand
3. how lazy the operator can be (missed successes)
4. how careless the operator can be (false positives, uniform and boundary-correlated)
5. how tight the success set is, how many demonstrations there are, and whether they are biased
6. critic steps per policy step, weight clipping, reward regularisation

## What it is not

An illustration of a mechanism, not evidence. The critic is a 2→32→32→1 tanh network with
weight-clipped weights ascending `mean f(demos) − mean f(negatives)`; the policy ascends
`∇ₓf`; both step every frame in your browser. Quantitative claims in the paper come from the
robot experiments, not from this page. The "what the offline sweeps say" panel reports numbers
measured with the same toy offline, at the defaults shown.

Two modelling choices are load-bearing and both are stated in the page: the expert is a finite
demonstration set so no policy mean can match it (without that non-realizability the game is a
damped system that converges on its own), and the operator's success set always contains the
demonstrations, since a demonstration is a success by definition.

## License

MIT, © the authors. See [LICENSE](LICENSE).
