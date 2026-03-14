# STORYBOARD: Engineering Design Optimization
## Visual Explainer Presentation
### Dark theme, fullscreen HTML/JS/CSS with animated SVG diagrams

---

## NARRATIVE ARC

**Central thesis**: Engineering design optimization systematically finds the best designs using gradient-based methods. The adjoint method, algorithmic differentiation, and the unified derivative equations make this computationally feasible — even for multidisciplinary systems with coupled physics.

**Thread**: Why optimization matters → gradient-based methods → computing gradients (FD → direct → adjoint → AD → unified framework) → multidisciplinary optimization (XDSM, MDF, coupled adjoint) → aerostructural wing example → state of the art.

**Target audience**: Graduate students and industry professionals in engineering.

---

## ACT 1: THE PROBLEM — Why Optimize? (Slides 1–6)

### Slide 1: Title
- "Engineering Design Optimization"
- Subtitle: "From Gradients to Multidisciplinary Systems"
- Based on Martins & Ning (2022)

### Slide 2: Why Optimization Matters
- 3 concrete examples with numbers: wing drag reduction, structural weight, turbine efficiency
- Martins quote on optimization goals
- Key insight: optimization replaces trial-and-error with mathematics

### Slide 3: The Optimization Problem
- General formulation: minimize f(x) subject to g(x) ≤ 0, bounds
- 3 cards: design variables (broadened), objective, constraints
- Reused structure from original slide 3

### Slide 4: What Makes It Hard?
- 3 challenge cards: computational cost, high dimensionality, coupled disciplines
- Key insight: these challenges motivate adjoint + MDO

### Slide 5: A Real Example: The Wing
- Split layout: text about aero-structural tradeoff + wing SVG
- Thin wing = low drag but high stress; thick wing = opposite
- Sets up MDO thread for Act 4

### Slide 6: Section Transition
- "How do we navigate this vast design space?"

---

## ACT 2: GRADIENT-BASED OPTIMIZATION (Slides 7–13)

### Slide 7: NURBS + Interactive Editor
- Consolidated NURBS intro (from original slides 4–7)
- Split layout: brief text + interactive NURBS editor
- IDs preserved: `nurbs-interactive`, `nurbs-ctrl-polygon`, `nurbs-curve`, `nurbs-ctrl-points`
- Key insight: local support → ideal for optimization

### Slide 8: The Optimization Loop
- Flowchart: Initial Design → Solve Physics → Compute Gradients → Update → Repeat
- Reused from original slide 9

### Slide 9: Gradient Descent
- Steepest descent on contour plot with zigzag
- Reused from original slide 10

### Slide 10: Interactive Gradient Descent
- Click to set start, watch zigzag path
- IDs preserved: `gd-interactive`, `gd-contours`, `gd-path`, `gd-points`
- Reused from original slide 11

### Slide 11: BFGS and SQP
- Consolidated from original slides 12–13
- BFGS card + SQP card + optimizer comparison SVG
- Nocedal & Wright quote, key insight

### Slide 12: All Methods Need Gradients
- Gradient vector formula
- "How do we compute these efficiently?"
- Reused from original slide 14

### Slide 13: Section Transition
- "Computing the compass — the gradient"
- Adapted from original slide 15

---

## ACT 3: COMPUTING DERIVATIVES — The Unified Framework (Slides 14–24)

### Slide 14: Finite Differences
- Perturbation formula, cost = (n_x + 1) × solve cost
- Citation: [Martins & Ning, 2022]
- Reused from original slide 16

### Slide 15: The Physics Model
- Implicit model: r(u; x) = 0
- Diagram: x → Solver → u → f(x,u)
- Added: wing CFD example in text
- Reused from original slide 17

### Slide 16: Total Derivative via Chain Rule
- df/dx = ∂f/∂x + (∂f/∂u)(du/dx)
- 3 cards explaining each term
- Reused from original slide 18

### Slide 17: The Linear System
- (∂r/∂u)(du/dx) = −(∂r/∂x)
- Key insight: linear system much cheaper than nonlinear
- Reused from original slide 19

### Slide 18: The Direct Method
- Forward mode: solve per design variable
- Matrix diagram with column highlights
- Reused from original slide 20

### Slide 19: The Adjoint Method
- Reverse mode: solve per function of interest
- Pironneau (1974) / Jameson (1988) history quote
- Matrix diagram with narrow ψ vector
- Reused from original slide 21

### Slide 20: One Solve → All Gradients
- Fan-out diagram: 1 adjoint solve → all df/dx_i
- Reused from original slide 22

### Slide 21: Interactive Cost Comparison
- Slider for n_x, bar chart (FD / Direct / Adjoint)
- IDs preserved: `cost-slider`, `cost-nx-label`, `cost-comparison-svg`, etc.
- Reused from original slide 23

### Slide 22: Algorithmic Differentiation (NEW)
- Two cards: Forward AD (tangent mode) vs Reverse AD (adjoint mode)
- Connection to backpropagation in deep learning
- Computational graph SVG: chain of operations with forward/reverse sweeps
- Griewank & Walther citation

### Slide 23: Unified Derivative Equations (NEW)
- UDE table: seed vector → method → cost scaling
- Four methods unified: FD, direct/forward, adjoint/reverse, AD
- Martins & Hwang (2013) quote
- Key insight: all methods are special cases of one framework

### Slide 24: Section Transition
- "Real problems have coupled disciplines"

---

## ACT 4: MULTIDISCIPLINARY DESIGN OPTIMIZATION (Slides 25–35)

### Slide 25: What is MDO?
- Venn diagram SVG: Aerodynamics ∩ Structures ∩ Controls
- Martins & Lambe (2013) quote
- Key insight: optimize the system, not individual components

### Slide 26: XDSM: Reading the Diagram
- Legend SVG explaining block types (optimizer, analysis, data)
- Lambe & Martins (2012) citation
- XDSM convention explanation

### Slide 27: XDSM: Single-Discipline (4 steps)
- Step 1: Optimizer block
- Step 2: Analysis block + design variables data
- Step 3: Objective/constraint feedback
- Step 4: Process flow numbers

### Slide 28: XDSM: Coupled Analysis / MDA (5 steps)
- Step 1: Aerodynamics block
- Step 2: Structures block
- Step 3: Loads data (Aero → Structures)
- Step 4: Displacement data (Structures → Aero)
- Step 5: Iteration loop + convergence annotation

### Slide 29: XDSM: MDF Architecture
- Full MDF XDSM: Optimizer → MDA (Aero ↔ Structures) → feedback
- Pro/con cards: robust but expensive inner loop
- Key insight: MDA ensures consistency at every optimization step

### Slide 30: Aerostructural Problem
- Split layout: text + wing coupling SVG (loads ↔ displacement)
- Problem stats: 311 design variables, 152 constraints
- Kenway et al. (2014) reference

### Slide 31: Aerostructural XDSM (4 steps)
- Full XDSM: SNOPT optimizer + ADflow (aero) + TACS (structures)
- Step-by-step reveal of optimization process

### Slide 32: The Coupled Adjoint
- Coupled adjoint equation block
- Kenway et al. (2019) quote
- Key insight: coupled adjoint extends adjoint efficiency to MDO

### Slide 33: Aerostructural Results
- Big number: 6.6% fuel burn reduction
- Before/after wing SVG
- Key insight: MDO finds designs no single-discipline approach could

### Slide 34: Applications Gallery
- 5 cards with concrete examples and numbers
- Adapted from original slide 28 with expanded content

### Slide 35: Section Transition
- "From components to full systems"

---

## ACT 5: TAKEAWAYS & REFERENCES (Slides 36–39)

### Slide 36: Key Takeaways
- 5 broadened takeaways (gradient methods, adjoint, AD, MDO, coupled adjoint)

### Slide 37: State of the Art (NEW)
- OpenMDAO framework
- MACH-Aero toolchain
- Software stack SVG: layers from optimizer → framework → solvers

### Slide 38: Historical Timeline (NEW)
- 1974–2022 timeline using `.timeline` CSS
- Key milestones: Pironneau, Jameson, BFGS, AD, OpenMDAO, MDO book

### Slide 39: References
- Expanded, categorized: Primary, Adjoint/Derivatives, MDO, Software
- Adapted from original slide 30

---

## SUMMARY COUNTS

- **39 slides** (vs 30 original)
- **~120 animation steps** (vs ~92 original)
- **~15 key-insight boxes** (every ~3 slides)
- **~10 expert quotes** (Martins, Nocedal, Jameson, Kenway, Griewank, etc.)
- **~11 inline citations**
- **19 new slides**, 15 reused/adapted, 5 consolidated

## INTERACTIVE ELEMENTS (IDs preserved)

| Element | Slide | IDs |
|---------|-------|-----|
| NURBS Editor | 7 | `nurbs-interactive`, `nurbs-ctrl-polygon`, `nurbs-curve`, `nurbs-ctrl-points` |
| Gradient Descent | 10 | `gd-interactive`, `gd-contours`, `gd-path`, `gd-points` |
| Cost Comparison | 21 | `cost-slider`, `cost-nx-label`, `cost-comparison-svg`, `cost-bar-fd`, etc. |

## XDSM SVG CONVENTION

- Diagonal blocks: `<rect rx="8">` with `fill="var(--bg-card)"`, colored stroke
- Off-diagonal data: `<polygon>` parallelograms
- Process flow: thick gray lines with circled numbers
- All elements wrapped in `<g class="anim-step">` for step-by-step reveal
- Consistent grid: ~180px column width, ~80px row height

## DESIGN SPECIFICATIONS

### Theme (unchanged from original)
- **Background**: Dark navy (#0a0e27)
- **Accent colors**: Cyan, Orange, Green, Pink, Purple, Yellow

### Navigation (unchanged)
- Arrow keys, F for fullscreen, progress bar, slide counter

### References
- Martins & Ning, *Engineering Design Optimization*, Cambridge, 2022
- Martins & Hwang, "Review and unification of methods for computing derivatives," AIAA J., 2013
- Martins & Lambe, "Multidisciplinary design optimization: A survey of architectures," Struct. Multidisc. Optim., 2013
- Lambe & Martins, "Extensions to the design structure matrix…," Struct. Multidisc. Optim., 2012
- Kenway et al., "Effective adjoint approaches for computational fluid dynamics," Prog. Aerosp. Sci., 2019
- Kenway et al., "Multipoint high-fidelity aerostructural optimization of a transport aircraft configuration," J. Aircraft, 2014
- Pironneau, "On optimum design in fluid mechanics," J. Fluid Mech., 1974
- Jameson, "Aerodynamic design via control theory," J. Sci. Comput., 1988
- Griewank & Walther, *Evaluating Derivatives*, SIAM, 2008
- Nocedal & Wright, *Numerical Optimization*, Springer, 2006
- Gray et al., "OpenMDAO: An open-source framework for multidisciplinary design, analysis, and optimization," Struct. Multidisc. Optim., 2019
