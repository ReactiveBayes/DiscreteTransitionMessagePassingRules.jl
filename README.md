# DiscreteTransitionMessagePassingRules

[![CI](https://github.com/ReactiveBayes/DiscreteTransitionMessagePassingRules.jl/actions/workflows/CI.yml/badge.svg?branch=main)](https://github.com/ReactiveBayes/DiscreteTransitionMessagePassingRules.jl/actions/workflows/CI.yml)
[![Docs: stable](https://img.shields.io/badge/docs-stable-blue.svg)](https://reactivebayes.github.io/DiscreteTransitionMessagePassingRules.jl/stable/)
[![Docs: dev](https://img.shields.io/badge/docs-dev-blue.svg)](https://reactivebayes.github.io/DiscreteTransitionMessagePassingRules.jl/dev/)
[![Coverage](https://codecov.io/gh/ReactiveBayes/DiscreteTransitionMessagePassingRules.jl/graph/badge.svg)](https://codecov.io/gh/ReactiveBayes/DiscreteTransitionMessagePassingRules.jl)
[![Code style: Runic](https://img.shields.io/badge/code_style-%E1%9A%B1%E1%9A%A2%E1%9A%BE%E1%9B%81%E1%9A%B2-black)](https://github.com/fredrikekre/Runic.jl)

The `DiscreteTransition` node, `out ~ Categorical(A[:, in, T1, …, Tn])`: a transition between
categoricals through a tensor `A` of probabilities, conditioned on any number of categoricals
`T`, with `A` known (a `PointMass`) or learned (a `DirichletCollection`). It is the transition and
emission node of hidden Markov models. As a tensor node, each of its rules is one tensor
contraction, written once for belief propagation, mean-field and structured factorisations and
any number of `T`s. It runs under the default algorithm and has an average energy.

```julia
using DiscreteTransitionMessagePassingRules, MessagePassingRulesBase, BayesBase, ExponentialFamily

result = @call_message_update_rule(
    node = DiscreteTransition, target = :out,
    m = (in = Categorical([0.5, 0.5]),), q = (a = PointMass([0.9 0.2; 0.1 0.8]),),
)
getresult(result)   # Categorical([0.55, 0.45])
```

```julia
import Pkg; Pkg.add("DiscreteTransitionMessagePassingRules")
```

- Documentation: <https://reactivebayes.github.io/DiscreteTransitionMessagePassingRules.jl/stable/>.
  `make docs` builds it locally, into `docs/build`.
- Tests: `make test` runs the suite as CI does, ending with the rule-coverage gate: every rule
  must be selected by some test. `make test test_args="name:rules"` selects items by tag, by
  name or by file; `make help` lists the other targets.
- Julia 1.10 or later. MIT licence.
