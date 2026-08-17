# 13. Conductivity

`Analysis > Conductivity`

Two transport quantities carried by two different things — ions and
electrons.

---

## Ionic

`Analysis > Conductivity > Ionic`

### The theory

The **Nernst–Einstein** relation converts a diffusion coefficient into
a conductivity:

```
σ = (n q² / k_B T) · D
```

| | |
|---|---|
| `n` | number density of the mobile ion, per m³ |
| `q` | its charge, `z·e` |
| `D` | diffusion coefficient, m²/s |

The physical content is that both diffusion and conduction are the same
ionic motion — diffusion driven by a concentration gradient, conduction
by an electric field — and the fluctuation–dissipation theorem relates
the response to the equilibrium fluctuation.

So this follows on from [molecular dynamics](11-molecular-dynamics.md):
you need a `D` first, and preferably an activation energy so you can
quote σ at a temperature you did not simulate.

### The correlation caveat

Nernst–Einstein assumes ions move **independently**. They do not.

Measured conductivity relates to the **charge** diffusion coefficient
(the collective motion of the whole ion population), while MSD gives the
**tracer** diffusion coefficient (following individual ions). The ratio
is the Haven ratio:

```
H_R = D_tracer / D_charge
```

`H_R < 1` when motions are correlated — as in essentially every real
superionic conductor, where ions move in concerted chains rather than
one at a time. The [Van Hove distinct part](11-molecular-dynamics.md)
is what shows you this directly.

Ignoring correlation typically **underestimates** conductivity, often by
a factor of two or more.

**Quote the Nernst–Einstein value as an estimate and say so.** For the
order-of-magnitude question — is this 10⁻³ or 10⁻⁶ S/cm — it is
entirely adequate.

### For context

A solid electrolyte needs roughly **10⁻³ S/cm at room temperature** to
be practical. Reaching that conclusion from a simulated `D` at
600–1000 K means extrapolating over a long range, so the activation
energy carries most of the weight:

```
σ(300 K) = σ(1000 K) · (1000/300) · exp[-(E_a/k_B)(1/300 - 1/1000)]
```

An error of 0.1 eV in `E_a` moves the room-temperature answer by about
an order of magnitude. Get `E_a` from three or more temperatures, not
two.

---

## Electronic

`Analysis > Conductivity > Electronic`

![The electronic conductivity dialog](images/conductivity-electronic.png)

### The theory

Electronic transport from the band structure, in the **constant
relaxation-time approximation** to the Boltzmann transport equation:

```
σ/τ  = e² ∫ (-∂f/∂ε) Σ_nk v_nk ⊗ v_nk δ(ε - ε_nk) dε

S    = (1/eT) · [ ∫ (-∂f/∂ε)(ε - μ) Σ v⊗v δ(ε-ε_nk) dε ] / [ ∫ (-∂f/∂ε) Σ v⊗v δ dε ]
```

where `v_nk = (1/ℏ) ∂ε_n/∂k` is the band velocity — the **slope** of the
band.

Two consequences worth internalising:

**Transport depends on the derivative of the bands**, not their
energies. A flat band contributes nothing to conduction however many
states it has. This is why a high DOS at E_F does not imply good
conductivity.

**Only states within a few `k_BT` of E_F matter**, because `-∂f/∂ε` is
sharply peaked there. Everything else is irrelevant to transport.

### The dense mesh requirement

Because transport weights band **slopes** near E_F, it needs a much
denser k-mesh than a total-energy calculation. A mesh that gives a
perfectly converged energy will give a badly converged Seebeck
coefficient. This is the most common error in transport calculations.

### σ/τ, not σ

The relaxation time `τ` is **not** obtainable from the band structure —
it depends on scattering from phonons, defects and boundaries. What
comes out is `σ/τ`, and converting to a conductivity requires supplying
a `τ`, typically fitted to an experimental measurement or taken as
~10⁻¹⁴ s.

**The Seebeck coefficient does not depend on `τ`** in this
approximation, since `τ` cancels between numerator and denominator. That
makes `S` the quantity worth trusting here.

If you are comparing thermoelectric candidates, compare `S` and the
power factor `S²σ/τ`, and be explicit that any absolute conductivity
carries an assumed `τ`.

### For a battery material, read it backwards

Here you usually want electronic conductivity to be **low** — a solid
electrolyte that conducts electrons is a short circuit that
self-discharges the cell.

The useful output is then not really the transport integral but the
**band gap** underneath it:

- gap > ~3 eV → negligible electronic conduction, good electrolyte
- small or no gap → disqualified as an electrolyte however well it
  conducts ions

For a **cathode** the requirement inverts: you need both good ionic
*and* good electronic conductivity, which is why cathodes are mixed
conductors and why poor electronic conductivity is routinely fixed with
a carbon coating rather than by changing the chemistry.

---

**Next:** [Plots and export](14-plots-and-export.md).
