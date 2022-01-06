# Planck.jl

[![Build Status](https://github.com/JuliaAstro/Planck.jl/actions/workflows/CI.yml/badge.svg?branch=main)](https://github.com/JuliaAstro/Planck.jl/actions/workflows/CI.yml?query=branch%3Amain)
[![PkgEval](https://juliaci.github.io/NanosoldierReports/pkgeval_badges/P/Planck.svg)](https://juliaci.github.io/NanosoldierReports/pkgeval_badges/report.html)
[![Coverage](https://codecov.io/gh/JuliaAstro/Planck.jl/branch/main/graph/badge.svg)](https://codecov.io/gh/JuliaAstro/Planck.jl)
[![License](https://img.shields.io/github/license/JuliaAstro/Planck.jl?color=yellow)](LICENSE)

[![Stable](https://img.shields.io/badge/docs-stable-blue.svg)](https://JuliaAstro.github.io/Planck.jl/stable)
[![Dev](https://img.shields.io/badge/docs-dev-blue.svg)](https://JuliaAstro.github.io/Planck.jl/dev)

Blackbody radiation curves, with support for Unitful.jl.

## Installation

## Usage

### Wien's law

Using [Optim.jl](https://github.com/JuliaNLSolvers/Optim.jl) we can numerically maximize the blackbody function to see how closely it agrees with [Wien's law](https://en.wikipedia.org/wiki/Wien%27s_displacement_law).

```julia
using Optim

# function to minimize
temp = 5796
f(X) = -blackbody(first(X), temp)

# without AD
res = Optim.optimize(f, [1e-7 * randn() + 5e-7], NelderMead())
# with AD
res_ad = Optim.optimize(f, [1e-7 * randn() + 5e-7], Newton(); autodiff=:forward)

lam = first(Optim.minimizer(res_ad))
@test lam ≈ 2.898e-3 / temp rtol=1e-4
```

## Contributing and Support

If you would like to contribute, feel free to open a [pull request](https://github.com/JuliaAstro/Planck.jl/pulls). If you want to discuss something before contributing, head over to [discussions](https://github.com/JuliaAstro/Planck.jl/discussions) and join or open a new topic. If you're having problems with something, please open an [issue](https://github.com/JuliaAstro/Planck.jl/issues).
