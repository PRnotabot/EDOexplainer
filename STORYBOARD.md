# STORYBOARD: Shape Optimization with the Adjoint Method
## Visual Explainer Presentation
### Dark theme, fullscreen HTML/JS/CSS with animated SVG diagrams

---

## NARRATIVE ARC

**Central thesis**: Shape optimization is about finding the best geometry for engineering performance. The adjoint method makes this computationally feasible by computing all gradients in a single solve — regardless of how many design variables describe the shape.

**Thread**: Start with why shape matters → how we describe shapes mathematically (NURBS) → how optimization navigates the design space (gradient-based methods) → why computing gradients is the bottleneck → how the adjoint method solves this → the full workflow.

---

## ACT 1: THE PROBLEM — Why Shape Optimization? (Slides 1-8)

### Slide 1: Title
- "Shape Optimization with the Adjoint Method"
- Subtitle: "From NURBS Control Points to Optimal Geometries"

### Slide 2: Why Shape Matters
- Small changes in shape → large changes in performance
- Airfoil drag, structural weight, heat transfer
- Visual: two airfoil shapes — blunt vs streamlined

### Slide 3: The Optimization Problem
- Minimize objective f(x) subject to constraints g(x) ≤ 0
- x = design variables, f = performance metric
- Visual: problem formulation display

### Slide 4: What Are Design Variables for Shapes?
- Need a mathematical parametrization
- Too few parameters = limited design freedom
- Too many = expensive optimization
- Visual: different parametrizations comparison

### Slide 5: NURBS — Control Points Define Curves
- Non-Uniform Rational B-Splines
- Control points define shape WITHOUT touching the curve
- Visual: control polygon + resulting smooth curve

### Slide 6: B-Spline Basis Functions
- Recursive definition (Cox–de Boor)
- Each control point has a region of influence
- Visual: basis functions plotted, showing local support

### Slide 7: Interactive NURBS Editor
- Drag control points to deform the shape
- See how local changes affect the curve
- INTERACTIVE: draggable SVG control points

### Slide 8: Section Transition
- "We can describe any shape with NURBS. Now how do we find the BEST shape?"

---

## ACT 2: GRADIENT-BASED OPTIMIZATION (Slides 9-16)

### Slide 9: The Optimization Loop
- Start with initial design → evaluate → compute gradient → update → repeat
- Visual: flowchart of optimization loop

### Slide 10: Gradient Descent — Follow the Slope
- p = −∇f (steepest descent direction)
- Visual: gradient vector on contour plot

### Slide 11: Interactive Gradient Descent
- INTERACTIVE: show optimizer path on 2D contour plot
- Demonstrate zigzagging behavior of steepest descent

### Slide 12: Better Methods — Conjugate Gradient & BFGS
- Use curvature information to avoid zigzag
- Quasi-Newton: approximate the Hessian
- Visual: comparison of optimizer paths

### Slide 13: Constrained Optimization
- Real problems have constraints (stress, volume, etc.)
- SQP: solve quadratic subproblems
- Visual: feasible region with optimizer path

### Slide 14: All Methods Need Gradients
- Every iteration needs ∂f/∂x for all design variables
- Shape optimization: hundreds or thousands of variables
- "How do we compute these gradients efficiently?"

### Slide 15: Section Transition
- "The optimizer knows WHERE to go — if you give it the gradient. But computing gradients is the real challenge."

---

## ACT 3: COMPUTING DERIVATIVES — The Adjoint Method (Slides 16-26)

### Slide 16: Finite Differences — The Simple Approach
- Perturb each variable, re-evaluate
- df/dx_i ≈ (f(x+hê_i) − f(x)) / h
- Visual: showing perturbation of each variable

### Slide 17: The Cost of Finite Differences
- Need n_x function evaluations (one per variable)
- Each evaluation = solve the physics (expensive!)
- Visual: bar chart of cost scaling

### Slide 18: The Physics Model
- Governing equations: r(u; x) = 0
- u = states (pressure, velocity, displacement)
- x = design variables (control point positions)
- f(x, u) = objective function
- Visual: the implicit model diagram

### Slide 19: Total Derivative via Chain Rule
- df/dx = ∂f/∂x + (∂f/∂u)(du/dx)
- Need du/dx — but u is implicitly defined by r=0
- Visual: dependency diagram

### Slide 20: The Linear System
- Differentiate r(u;x)=0 → (∂r/∂u)(du/dx) = −(∂r/∂x)
- Can solve for du/dx without re-solving nonlinear system!
- Visual: matrix equation with sizes annotated

### Slide 21: The Direct Method
- Solve (∂r/∂u)φ = ∂r/∂x_i for each design variable i
- Then df/dx = ∂f/∂x − (∂f/∂u)φ
- Cost: n_x linear solves
- Visual: matrix diagram showing n_x columns

### Slide 22: The Adjoint Method — The Key Insight
- Instead of solving with ∂r/∂x (one per design variable)
- Solve with ∂f/∂u (one per function of interest)
- (∂r/∂u)ᵀψ = (∂f/∂u)ᵀ — only n_f solves!
- Visual: transposed matrix diagram

### Slide 23: Adjoint Gives ALL Gradients at Once
- df/dx = ∂f/∂x − ψᵀ(∂r/∂x)
- One adjoint solve → gradient w.r.t. ALL design variables
- Visual: one solve fan-out to all derivatives

### Slide 24: Direct vs Adjoint — Cost Comparison
- INTERACTIVE: slider for n_x, showing cost bars
- Direct: cost ∝ n_x, Adjoint: cost ∝ n_f
- For shape optimization: n_x >> n_f → adjoint wins

### Slide 25: Why Adjoint for Shape Optimization
- Typical: 500 design variables, 1 objective + a few constraints
- Finite differences: 500 solves
- Direct method: 500 solves
- Adjoint method: 1-5 solves
- Visual: dramatic cost comparison

### Slide 26: Section Transition
- "The adjoint method makes shape optimization computationally feasible."

---

## ACT 4: THE FULL PICTURE (Slides 27-31)

### Slide 27: The Complete Workflow
- Parametrize (NURBS) → Mesh → Solve Physics → Adjoint Solve → Gradient → Optimizer → Update Shape → Repeat
- Visual: full pipeline diagram

### Slide 28: Shape Optimization in Action
- Show airfoil shape evolving from initial to optimized
- Drag reduces, lift maintained
- Visual: animated optimization history

### Slide 29: Applications
- Aerospace (wings, engines), Automotive (body), Turbomachinery (blades), Structures (brackets)
- Visual: grid of application examples

### Slide 30: Key Takeaways
- 5 key points with icons
  1. Shape parametrization with NURBS gives smooth, flexible design freedom
  2. Gradient-based optimization efficiently navigates high-dimensional design spaces
  3. The adjoint method computes ALL gradients in cost independent of number of variables
  4. This makes large-scale shape optimization computationally feasible
  5. The combination of NURBS + adjoint + gradient-based optimization is the state of the art

### Slide 31: References
- MDO Book (Martins & Ning, 2022)
- Key papers on adjoint methods
- Pironneau (1974), Jameson (1988), Martins (2020)

---

## SVG ANIMATION INVENTORY

| # | Animation | Slide | Complexity |
|---|-----------|-------|------------|
| 1 | Airfoil comparison | 2 | Simple |
| 2 | NURBS curve + control polygon | 5 | Medium |
| 3 | Basis functions plot | 6 | Medium |
| 4 | Interactive NURBS editor | 7 | Complex |
| 5 | Optimization loop flowchart | 9 | Simple |
| 6 | Gradient on contour plot | 10 | Medium |
| 7 | Interactive gradient descent | 11 | Complex |
| 8 | Optimizer comparison | 12 | Medium |
| 9 | Implicit model diagram | 18 | Medium |
| 10 | Matrix equation diagram | 20-22 | Medium |
| 11 | Adjoint fan-out diagram | 23 | Medium |
| 12 | Interactive cost comparison | 24 | Complex |
| 13 | Full pipeline diagram | 27 | Medium |
| 14 | Airfoil optimization animation | 28 | Complex |

---

## DESIGN SPECIFICATIONS

### Theme (matching reference)
- **Background**: Dark navy (#0a0e27)
- **Text**: White (#ffffff) for headings, light gray (#b0b8d0) for body
- **Accent colors**:
  - Cyan (#00d4ff) — primary accent, NURBS, curves
  - Orange (#ff6b35) — gradients, derivatives
  - Green (#00e676) — convergence, optimal
  - Pink/Red (#ff4081) — cost, expensive
  - Purple (#b388ff) — adjoint-specific
  - Yellow (#ffd740) — highlights, key insights

### Navigation
- Arrow keys: Left/Right for slides
- Right arrow advances animation steps within a slide, then next slide
- F: Toggle fullscreen
- Progress bar at bottom
- Slide counter: bottom-right

### References
- Martins & Ning, "Engineering Design Optimization," Cambridge University Press, 2022
- Pironneau, "On optimum design in fluid mechanics," 1974
- Jameson, "Aerodynamic design via control theory," 1988
- Martins, "Perspectives on aerodynamic design optimization," 2020
- Haftka & Grandhi, "Structural shape optimization — A survey," 1986
