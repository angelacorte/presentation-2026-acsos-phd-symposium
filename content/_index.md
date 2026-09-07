+++

title = "Toward a Collective Robotic Operating System"
description = "ACSOS 2026 PhD Symposium presentation"
outputs = ["Reveal"]

+++

{{< slide class="title-slide" transition="fade" >}}

<div class="title-layout">
<div class="title-copy">

<p class="eyebrow">@ ACSOS 2026 · PhD Symposium</p>

# Towards Collective Robotic Operating Systems

<p class="subtitle">Aggregate Computing for adaptive robot swarms</p>

<p class="author"><strong>Angela Cortecchia</strong><br>
Supervisor: Prof. Danilo Pianini <br>Co-supervisor: Prof. Mirko Viroli</p>

<p class="title-mail"><a href="mailto:angela.cortecchia@unibo.it">angela.cortecchia@unibo.it</a></p>

<img class="title-logo" src="images/DIP INFORMATICA-SCIENZA E INGEGNERIA_DISI_EN.svg" alt="Department of Computer Science and Engineering, University of Bologna">

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

A robotic collective must pursue a **system-level goal** with only local views and
**no centralized point of coordination**.

<div class="challenge-list">
<p>Robots are heterogeneous: they move, fail, join, and leave</p>
<p>Connectivity and sensing change at runtime</p>
<p>Unsafe transients can cause physical damage</p>
</div>

<p class="takeaway">The collective needs runtime support, not only a coordination algorithm.</p>

{{% /col %}}
{{% col class="visual-col" %}}

<img class="hero-image" src="images/drones_changing-formation.png" alt="Drones changing formation around obstacles">

{{% /col %}}
{{% /multicol %}}

{{% note %}}
Timing: 55 seconds. Emphasize that mobility and failures change the computational structure during execution, and that there is nobody in the middle to re-plan for everyone. The operating layer must react while the robots remain physically safe.
{{% /note %}}

---

{{< slide class="aggregate-slide" transition="fade" >}}

<p class="eyebrow">Programming abstraction</p>

# One program for the whole collective

{{% multicol class="split" %}}
{{% col class="copy-col" %}}

<p class="today"><strong>Usually, each robot is programmed individually</strong> — a common example is ROS.
With hundreds of robots, that does not scale.</p>

With **Aggregate Computing** the collective is programmed as a whole, and the same
program runs decentralized on every device, which repeatedly:

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
Timing: 60 seconds. Open on the contrast: today the unit of programming is the robot, and it does not scale. Then computational fields as values distributed across devices. Aggregate Computing raises the abstraction level without introducing a central controller.
{{% /note %}}

---

{{< slide class="gap-slide" transition="fade" >}}

<p class="eyebrow">Research gap</p>

# Aggregate Computing programs the collective, but does not manage it

<div class="comparison">
<div class="comparison-side">
<h3>An aggregate application today</h3>
<p>One collective program, deployed once</p>
<ul>
<li>A single behavior runs on each device</li>
<li>No preemption, no lifecycle management</li>
<li>Self-stabilization guarantees recovery <em>eventually</em></li>
</ul>
</div>
<div class="comparison-divider" aria-hidden="true"></div>
<div class="comparison-side collective-side">
<h3>What a robotic mission needs</h3>
<p>Several behaviors, changing while the swarm flies</p>
<ul>
<li>Concurrent applications on the same devices</li>
<li>An authorized operator that can stop or switch them</li>
<li>Constraints that hold <em>during</em> the transient</li>
</ul>
</div>
</div>

<p class="takeaway centered">The runtime must manage computations whose membership and physical footprint change over time.</p>

{{% note %}}
Timing: 60 seconds. This is the gap the paper states: typical Aggregate Computing applications run one algorithm per device, with no preemption and no lifecycle for multiple collective applications, and eventual consistency is not enough when a transient state is already unsafe. Concrete example: surveillance drones that law enforcement must be able to stop or redirect mid-mission. The OS analogy is a design lens, not a claim that every traditional OS mechanism transfers directly.
{{% /note %}}

---

{{< slide class="vision-slide" transition="fade" >}}

<p class="eyebrow">PhD research vision</p>

# Lifting operating-system services to the collective

<div class="vision-statement">
<span class="vision-label">CROS</span>
<p>A <strong>Collective Robotic Operating System</strong> built on Aggregate Computing</p>
</div>

<div class="os-map">
<div class="os-row">
<span class="os-cap">Resource management</span>
<span class="os-mean">Structures and resources grow where the collective needs them</span>
<span class="os-state">investigated</span>
</div>
<div class="os-row">
<span class="os-cap">Monitoring</span>
<span class="os-mean">Collective state estimated from distributed, unreliable observations</span>
<span class="os-state">investigated</span>
</div>
<div class="os-row">
<span class="os-cap">Adaptation</span>
<span class="os-mean">Tasks redistributed at runtime when a device is lost</span>
<span class="os-state">investigated</span>
</div>
<div class="os-row">
<span class="os-cap">Shared state</span>
<span class="os-mean">Agreement between processes occupying different regions</span>
<span class="os-state">investigated</span>
</div>
<div class="os-row">
<span class="os-cap">Safety</span>
<span class="os-mean">Physical constraints enforced while the collective is still moving</span>
<span class="os-state">investigated</span>
</div>
<div class="os-row open">
<span class="os-cap">Preemption &amp; lifecycle</span>
<span class="os-mean">Start, stop and switch collective processes without redeploying</span>
<span class="os-state">open</span>
</div>
<div class="os-row open">
<span class="os-cap">Permissions</span>
<span class="os-mean">Who is authorized to change the behavior of the collective</span>
<span class="os-state">open</span>
</div>
</div>

<p class="research-question">How can reusable runtime mechanisms keep collective behavior manageable while robots, goals, and networks change?</p>

{{% note %}}
Timing: 65 seconds. Read the left column: these are the words an operating system already has, mapped onto a collective. Five have been investigated and the next slide shows them. Preemption and permissions are the two that Aggregate Computing does not offer at all today, and they are the reason this research exists: an authorized operator must be able to stop or redirect a swarm mid-mission.
{{% /note %}}

---

{{< slide class="portfolio-slide" transition="fade" >}}

<p class="eyebrow">Investigated services &mdash; 1 of 3</p>

# Organising the collective in space

<div class="result-grid pair">
<figure>
<img src="images/oneroot.gif" alt="FieldVMC structures growing and branching from local interactions">
<figcaption><strong>Resource management</strong><span>FieldVMC</span>
<span class="detail">Structures grow, branch and repair from a local flow of resources, with no global blueprint.</span>
<span class="detail alt">Resources are routed towards the most successful area of the network: the shape is the outcome of a competition, not of a plan.</span>
</figcaption>
</figure>
<figure>
<img src="images/replanning.gif" alt="A swarm redistributing tasks after losing a robot">
<figcaption><strong>Adaptation</strong><span>Runtime replanning</span>
<span class="detail">A mission is assigned to the swarm; when a robot is lost, its tasks are redistributed among the survivors.</span>
<span class="detail alt">The plan is repaired by the collective while it operates, without re-running a global planner.</span>
</figcaption>
</figure>
</div>

{{% note %}}
Timing: 70 seconds. Two contributions, one minute of speaking. On FieldVMC insist on the second line: nobody designs the shape, it emerges from where the resources flow. On replanning insist that no planner is re-run: the swarm repairs its own plan while flying.
{{% /note %}}

---

{{< slide class="portfolio-slide" transition="fade" >}}

<p class="eyebrow">Investigated services &mdash; 2 of 3</p>

# Knowing what is happening, and agreeing on it

<div class="result-grid pair">
<figure>
<img src="images/dpf.gif" alt="Field-based distributed particle filtering tracking multiple targets">
<figcaption><strong>Monitoring</strong><span>Field-based distributed particle filtering</span>
<span class="detail">Several targets tracked from noisy observations, with observers that move and lose connectivity.</span>
<span class="detail alt">Where fusion happens, who leads, how far information travels: coordination is decoupled from the filtering logic, so it can be changed without redesigning the estimator.</span>
</figcaption>
</figure>
<figure>
<img src="images/gossip.gif" alt="Self-stabilizing min-max gossip converging over a network">
<figcaption><strong>Shared state</strong><span>Self-stabilizing min&ndash;max gossip</span>
<span class="detail">The best value in the network wins, and the collective converges to it from any state.</span>
<span class="detail alt">Each message carries the path of nodes that acknowledged it: that is what lets stale contributions be pruned, which classical min&ndash;max gossip cannot do.</span>
</figcaption>
</figure>
</div>

{{% note %}}
Timing: 70 seconds. On the DPF, the point is not the filter but the decoupling: the same estimator can be centralised, leader-based or fully decentralised by changing the coordination pattern. On the gossip, say plainly that monotonic min-max cannot retract a value once merged, and that the acknowledgement path is what makes retraction possible; it is proved self-stabilizing and shipped as a Collektive library.
{{% /note %}}

---

{{< slide class="filter-slide" transition="fade" >}}

<p class="eyebrow">Investigated services &mdash; 3 of 3</p>

# A safety filter between collective strategy and actuation

<div class="filter-layout">
<div class="filter-diagram">
<img src="images/architecture-web.svg" alt="Architecture combining an aggregate strategy layer with a distributed safety filter">
<div class="layer-explainer">
<p><strong>Aggregate program</strong><br>Computes the nominal swarm command <em>u<sub>nom</sub></em></p>
<p><strong>CLF/CBF safety filter</strong><br>Refines it into a feasible command <em>u</em> before actuation</p>
</div>
</div>
<figure class="filter-demo">
<img src="images/follow-leader.gif" alt="Robot clusters merging and following a common leader">
<figcaption><strong>Dynamic leader election</strong><span>Connectivity preserved while separate clusters merge onto one leader</span></figcaption>
</figure>
</div>

<p class="scope-note"><strong>Scope:</strong> proof-of-concept simulations; quantitative scalability and overhead remain future work. Collective strategy and physical safety stay separate concerns.</p>

{{% note %}}
Timing: 70 seconds. CLFs encode convergence objectives, CBFs encode safety constraints, and the local and pairwise quadratic programs run distributed. Keep it to the architecture and one scenario: clusters merge onto a common leader and the filter preserves the communication links while they do. The full treatment is the technical-track talk, and this is the place to invite people to it out loud. State the scope honestly.
{{% /note %}}

---

{{< slide class="closing-slide" transition="fade" >}}

<p class="eyebrow">Wrap-up</p>

# Takeaways and future work

<div class="closing-layout">
<div class="wrap-up">

<div class="wrap-col">
<p class="wrap-label">Takeaways</p>
<ul class="closing-list">
<li>For swarm missions the right unit of programming is the <strong>collective</strong>, not the robot;</li>
<li>Aggregate Computing gives that abstraction, but no way to <strong>manage</strong> what it runs;</li>
<li>Five operating-system services already have a decentralized mechanism behind them.</li>
</ul>
</div>

<div class="wrap-col next-col">
<p class="wrap-label">Future work</p>
<ul class="closing-list">
<li>Combine spatial organization and safety: <strong>complex shapes that grow and move</strong> without unsafe transients;</li>
<li>Add the two missing services: <strong>preemption and lifecycle</strong>, and <strong>permissions</strong> over collective behavior;</li>
<li>Integrate the mechanisms into a <strong>CROS prototype</strong> in Collektive.</li>
</ul>
</div>

</div>
<div class="closing-mark">
<img src="images/qr.png" alt="QR code linking to my personal portfolio">
<p>Personal portfolio</p>
</div>
</div>

<p class="final-line">Make the swarm programmable as one system, while keeping its adaptation explicit and safe.</p>

{{% note %}}
Timing: 60 seconds. Read the takeaways, then the future work. On the second future-work point, say that preemption and permissions are the two rows left open in the vision map, and that aggregate processes already give a model for concurrent collective computations: what is missing is how such a process expands and contracts across space. The QR code is the personal portfolio, so point at it while inviting questions.
{{% /note %}}
