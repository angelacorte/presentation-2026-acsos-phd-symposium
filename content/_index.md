+++

title = "Toward a Collective Robotic Operating System"
description = "ACSOS 2026 PhD Symposium presentation"
outputs = ["Reveal"]

+++

{{< slide class="title-slide" transition="fade" >}}

<div class="title-layout">
<div class="title-copy">

<p class="eyebrow">ACSOS 2026 · PhD Symposium</p>

# Toward a Collective Robotic Operating System

<p class="subtitle">Aggregate Computing for adaptive robot swarms</p>

<p class="author"><strong>Angela Cortecchia</strong><br>University of Bologna · DISI</p>

</div>
<div class="title-visual">
<img src="images/drones_avoiding_formation.png" alt="A robot swarm reorganizing around obstacles">
</div>
</div>

{{% note %}}
Timing: 30 seconds. Introduce the research goal: make a swarm programmable and manageable as one adaptive system.
{{% /note %}}

---

{{< slide class="challenge-slide" transition="fade" >}}

<p class="eyebrow">The engineering problem</p>

# A swarm keeps changing while it operates

{{% multicol class="split wide-gap" %}}
{{% col class="copy-col" %}}

A robotic collective must pursue a **system-level goal** while each robot has only a local view.

<div class="challenge-list">
<p>{{< frag c="Robots move, fail, join, and leave" >}}</p>
<p>{{< frag c="Connectivity and sensing change at runtime" >}}</p>
<p>{{< frag c="Unsafe transients can cause physical damage" >}}</p>
</div>

<p class="takeaway">The collective needs runtime support, not only a coordination algorithm.</p>

{{% /col %}}
{{% col class="visual-col" %}}

<img class="hero-image" src="images/drones_changing-formation.png" alt="Drones changing formation around obstacles">

{{% /col %}}
{{% /multicol %}}

{{% note %}}
Timing: 50 seconds. Emphasize that mobility and failures change the computational structure during execution. The operating layer must react while the robots remain physically safe.
{{% /note %}}

---

{{< slide class="aggregate-slide" transition="fade" >}}

<p class="eyebrow">Programming abstraction</p>

# Aggregate Computing programs the collective

{{% multicol class="split" %}}
{{% col class="copy-col" %}}

Each device repeatedly:

1. senses local information;
2. exchanges data with its neighbors;
3. runs the same aggregate program;
4. acts on its local result.

<p class="takeaway">Local executions compose into a global behavior.</p>

{{% /col %}}
{{% col class="visual-col collective-visual" %}}

<img src="images/collective.svg" alt="Local device interactions producing collective behavior">

<p class="image-caption">One program, distributed execution, collective outcome</p>

{{% /col %}}
{{% /multicol %}}

{{% note %}}
Timing: 55 seconds. Explain computational fields as values distributed across devices. Aggregate Computing raises the abstraction level without introducing a central controller.
{{% /note %}}

---

{{< slide class="gap-slide" transition="fade" >}}

<p class="eyebrow">Research gap</p>

# A programming model does not yet provide an operating layer

<div class="comparison">
<div class="comparison-side">
<h3>Traditional operating system</h3>
<p>Runs processes on one machine</p>
<ul>
<li>Lifecycle and preemption</li>
<li>Interprocess communication</li>
<li>Resource access</li>
</ul>
</div>
<div class="comparison-divider" aria-hidden="true"></div>
<div class="comparison-side collective-side">
<h3>Collective counterpart</h3>
<p>Runs aggregate processes across space</p>
<ul>
<li>Distributed lifecycle management</li>
<li>Communication across regions</li>
<li>Collective sensing and actuation</li>
</ul>
</div>
</div>

<p class="takeaway centered">The runtime must manage computations whose membership and physical footprint change over time.</p>

{{% note %}}
Timing: 55 seconds. Use the OS analogy as a design lens, not as a claim that every traditional OS mechanism transfers directly.
{{% /note %}}

---

{{< slide class="vision-slide" transition="fade" >}}

<p class="eyebrow">PhD research vision</p>

# Collective processes as the unit of management

<div class="vision-statement">
<span class="vision-label">CROS</span>
<p>A <strong>Collective Robotic Operating System</strong> built on Aggregate Computing</p>
</div>

<div class="capability-line">
<span>Concurrent applications</span>
<span>Runtime adaptation</span>
<span>Transient safety</span>
<span>Collective sensing</span>
<span>Resilient state</span>
</div>

<p class="research-question">How can reusable runtime mechanisms keep collective behavior manageable while robots, goals, and networks change?</p>

{{% note %}}
Timing: 50 seconds. Present CROS as the long-term research vision. The capabilities form the evaluation dimensions for the incremental work.
{{% /note %}}

---

{{< slide class="portfolio-slide" transition="fade" >}}

<p class="eyebrow">Progress so far</p>

# Four building blocks for the operating layer

<div class="contribution-grid">
<figure>
<img src="images/oneroot.gif" alt="FieldVMC structures emerging from local interactions">
<figcaption><strong>Spatial organization</strong><span>FieldVMC</span></figcaption>
</figure>
<figure>
<img src="images/replanning.gif" alt="Robot teams replanning after a mission change">
<figcaption><strong>Runtime replanning</strong><span>Field-based missions</span></figcaption>
</figure>
<figure>
<img src="images/gossip.gif" alt="A distributed network exchanging gossip state">
<figcaption><strong>Resilient state</strong><span>Self-stabilizing gossip</span></figcaption>
</figure>
<figure>
<img src="images/dpf.gif" alt="Distributed particle filtering over a sensor network">
<figcaption><strong>Collective sensing</strong><span>Field-based DPF</span></figcaption>
</figure>
</div>

<p class="takeaway centered">Each problem contributes a mechanism that can become part of a shared runtime.</p>

{{% note %}}
Timing: 65 seconds. Give one sentence per contribution. FieldVMC supports asynchronous organization. Replanning redistributes tasks. Gossip retracts obsolete state after faults. Field-based DPF separates estimation from coordination choices.
{{% /note %}}

---

{{< slide class="transient-slide" transition="fade" >}}

<p class="eyebrow">Open problem</p>

# Eventual recovery leaves a safety gap

{{% multicol class="split wide-gap" %}}
{{% col class="copy-col" %}}

Self-stabilizing programs guarantee recovery **after perturbations stop**.

During convergence, a robot may still:

- collide with another robot;
- hit an obstacle;
- break a required communication link.

<p class="takeaway warning">Physical constraints must hold during adaptation.</p>

{{% /col %}}
{{% col class="visual-col" %}}

<img class="hero-image" src="images/drones_eventual_consistency.png" alt="A swarm temporarily changing its formation near obstacles">

<p class="image-caption">The collective may still be reorganizing when a command reaches an actuator</p>

{{% /col %}}
{{% /multicol %}}

{{% note %}}
Timing: 60 seconds. Contrast eventual convergence with invariants that must hold at every instant. This motivates the paper's safety-filter architecture.
{{% /note %}}

---

{{< slide class="architecture-slide" transition="fade" >}}

<p class="eyebrow">Latest contribution</p>

# Toward Safe Aggregate Computing

<div class="architecture-wrap">
<img src="images/architecture.pdf" alt="Architecture combining an aggregate strategy layer with a distributed safety filter">
</div>

<div class="layer-explainer">
<p><strong>Aggregate program</strong><br>Computes the nominal swarm command <em>u<sub>nom</sub></em></p>
<p><strong>CLF/CBF safety filter</strong><br>Refines it into a feasible command <em>u</em> before actuation</p>
</div>

<p class="takeaway centered">Collective strategy and physical safety remain separate concerns.</p>

{{% note %}}
Timing: 80 seconds. Explain that CLFs encode convergence objectives and CBFs encode safety constraints. The local and pairwise quadratic programs run in a distributed fashion. The filter minimally modifies the nominal command when the active constraints are feasible.
{{% /note %}}

---

{{< slide class="results-slide" transition="fade" >}}

<p class="eyebrow">Proof of concept</p>

# The filter preserves active constraints in simulation

<div class="result-grid">
<figure>
<img src="images/different-targets.gif" alt="Two robot groups reaching different targets while avoiding obstacles">
<figcaption><strong>Different targets</strong><span>Collision and obstacle avoidance</span></figcaption>
</figure>
<figure>
<img src="images/follow-leader.gif" alt="Robot clusters merging and following a common leader">
<figcaption><strong>Dynamic leader election</strong><span>Connectivity preservation</span></figcaption>
</figure>
</div>

<p class="scope-note"><strong>Current scope:</strong> proof-of-concept simulations. Quantitative scalability and overhead evaluation remain future work.</p>

{{% note %}}
Timing: 70 seconds. Describe the two demonstrated scenarios. State the scope clearly: the paper shows feasibility in simulation and does not yet provide a quantitative performance evaluation.
{{% /note %}}

---

{{< slide class="closing-slide" transition="fade" >}}

<p class="eyebrow">Next research step</p>

# A shared runtime for managed collective adaptation

<div class="closing-layout">
<div>
<p class="closing-lead">Integrate the building blocks into a runtime that can:</p>
<ul class="closing-list">
<li>run and preempt multiple aggregate processes;</li>
<li>share state across dynamic regions;</li>
<li>switch strategies while preserving safety.</li>
</ul>
<p class="future-note"><strong>Planned extension:</strong> adaptive navigation policies that escape local minima, then resume the original objective.</p>
</div>
<div class="closing-mark">
<img src="images/qr.png" alt="QR code linking to the project materials">
<p>Code and experiments</p>
</div>
</div>

<p class="final-line">Make the swarm programmable as one system, while keeping its adaptation explicit and safe.</p>

{{% note %}}
Timing: 45 seconds. Close on the integration goal. Clarify that strategy switching around local minima is planned work, not a result of the current paper. Leave roughly 30 seconds of buffer within the 10-minute slot.
{{% /note %}}
