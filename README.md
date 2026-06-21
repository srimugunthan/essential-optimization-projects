
# Essential Optimization Projects

---

## Summary: Problem Class Coverage

| # | Problem Class | Project(s) | Method(s) | Coverage |
|---|---|---|---|---|
| 1 | Stochastic & Robust Optimization | Fleet Assignment Problem | Two-Stage Stochastic Programming, Robust Optimization | ✅ Covered |
| 2 | Stochastic Dynamic Programming / MDP | Seafood Distribution Center Stocking | Stochastic DP, Markov Decision Processes | ✅ Covered |
| 3 | Dynamic Programming / Revenue Management | Airline Seat Allocation | DP, EMSRb Algorithm | ✅ Covered |
| 4 | Combinatorial Optimization (Assignment) | Dinner Seating Arrangement | MILP, Constraint Programming | ✅ Covered |
| 5 | Network / Graph Algorithms | Cryptocurrency & Forex Arbitrage Search | Bellman-Ford, Floyd-Warshall | ✅ Covered |
| 6 | Linear Programming | MAD Portfolio Optimization | LP with auxiliary variable linearization | ✅ Covered |
| 7 | MILP — Workforce Scheduling | Workforce Shift Scheduling | MILP, Column Generation | ✅ Covered |
| 8 | MILP — Trajectory / Path Planning | EV Recharging Strategy | MILP, Shortest Path Variants | ✅ Covered |
| 9 | Constraint Programming | Machine & Job Shop Scheduling | CP, Asymmetric MILP | ✅ Covered |
| 10 | MILP — Location / Allocation | Facility Location Problem | MILP (binary + continuous variables) | ✅ Covered |
| 11 | Nonlinear & Convex Optimization | Power Grid Economic Dispatch | SOCP, SDP, QP (AC/DC OPF) | ✅ Covered |
| 12 | Multi-Objective Optimization / Pareto Frontier | Sustainable Supply Chain Design | Epsilon-Constraint, Weighted Sum, NSGA-II | ✅ Covered |
| 13 | Simulation-Based Optimization | ER Staff and Bed Allocation | Discrete-Event Simulation + Bayesian Optimization / Metaheuristics | ✅ Covered |
| 14 | Integer Programming Classics | Cloud Resource Bin Packing & Ad Slot Selection | MILP, LP Relaxation + Rounding, Greedy Set Cover | ✅ Covered |
| 15 | Network Design & Min-Cost Flow | Financial Settlement Network Optimization | Min-Cost Flow, Network Simplex, MILP | ✅ Covered |
| 16 | Reinforcement Learning as Optimization | Dynamic Pricing for Ride-Hailing / E-Commerce | PPO, SAC, Offline Policy Evaluation | ✅ Covered |
| — | Routing & Transportation (TSP / VRP) | — | Vehicle Routing Problem, TSP | ❌ Not Yet Covered |
| — | Metaheuristics (Large-Scale Heuristic Search) | — | Simulated Annealing, Tabu Search, Large Neighbourhood Search | ⚠️ Partial (used inside Sim-Based Opt.) |

---

## 1. Uncertainty & Dynamic Problems

### Fleet Assignment Problem

**Problem Description:** An airline needs to assign specific aircraft types (e.g., Boeing 737, Airbus A320) to scheduled flight legs across its entire network. Each aircraft type has a different passenger capacity, fuel efficiency, and operating cost. The primary challenge is accounting for real-world uncertainty, such as weather delays, unexpected maintenance, and fluctuating passenger demand, which can cause costly schedule disruptions.

**Optimization Method:** Two-Stage Stochastic Programming or Robust Optimization. You model the first-stage decision (assigning aircraft types to routes) and second-stage recourse decisions (delays, cancellations, or swapping aircraft) under a set of uncertain schedule disruption scenarios.

**Validation Metrics:**

- **MIP Gap:** Ensure the Mixed-Integer Programming (MIP) gap is within an acceptable threshold (e.g., < 1%).
- **Value of the Stochastic Solution (VSS):** Measures how much better your stochastic model performs compared to a deterministic model using average delay times.
- **Schedule Reliability Rate:** Out-of-sample simulation testing to ensure the chosen fleet assignment doesn't cause cascading delays under new, unmodeled schedule friction.

---

### Seafood Distribution Center Stocking

**Problem Description:** A distribution center manages highly perishable inventory (like fresh seafood) with a very short shelf life. If the manager orders too much inventory, it spoils and must be thrown away, resulting in a financial loss. If they order too little, they miss out on sales and risk damaging relationships with grocery or restaurant clients due to stockouts. Demand and market supply prices fluctuate daily.

**Optimization Method:** Stochastic Dynamic Programming or Markov Decision Processes (MDP). Because seafood is highly perishable, inventory levels must be optimized dynamically across time steps where supply and demand are modeled as random variables.

**Validation Metrics:**

- **Spoilage Rate / Waste Percentage:** The volume of inventory that expires before being sold.
- **Service Level (Fill Rate):** The percentage of customer demand met without stockouts.
- **Inventory Turnover Ratio:** Ensures the optimal policy matches the physical shelf-life reality.

---

### Airline Seat Allocation

**Problem Description:** A single flight has a fixed capacity of seats, but passengers arrive over a rolling booking window. Leisure travelers tend to book early and look for cheap fares, while lucrative business travelers book at the last minute and are willing to pay premium prices. The airline must dynamically decide whether to accept a current low-fare booking request or reject it to "protect" that seat for a potential high-fare passenger arriving later.

**Optimization Method:** Dynamic Programming via Dynamic Leg-Based Booking Limits or Network Revenue Management (EMSRb algorithm). This calculates the marginal value of an extra seat (shadow price/protection level) as booking requests arrive over time.

**Validation Metrics:**

- **Yield / Revenue Per Available Seat Mile (RASM):** Compares optimized revenue against baseline historical booking limits.
- **Spill and Spoilage Rates:** *Spill* measures lost revenue from turning away customers too early; *Spoilage* measures empty seats left on departure. A balanced solution minimizes both.

---

## 2. Combinatorial & Network Problems

### Dinner Seating Arrangement

**Problem Description:** Organizers of a large event or wedding need to assign a set of guests to a fixed number of tables, each with a maximum seating capacity. Guests have pre-existing relationships: some pairs must sit together (e.g., couples), some should sit together (e.g., coworkers), and others must be kept apart due to interpersonal conflicts. The goal is to maximize overall guest compatibility and comfort.

**Optimization Method:** Mixed-Integer Linear Programming (MILP) or Constraint Programming (CP). Guests and tables are mapped using binary decision variables (x_ig = 1 if guest i sits at table g). CP is highly efficient here due to the highly constrained, non-linear nature of social compatibility metrics.

**Validation Metrics:**

- **Feasibility Check:** Binary confirmation that every guest is assigned to exactly one table, and table capacities are strictly respected.
- **Total Affiliation Score / Conflict Count:** Summing the compatibility weights of adjacent guests to verify maximum satisfaction or zero active conflicts.

---

### Cryptocurrency & Forex Arbitrage Search

**Problem Description:** In financial and digital asset markets, the same asset or currency may be traded across multiple pairs or exchanges simultaneously. Due to slight inefficiencies or delays in market updates, a loop of trades (e.g., USD → EUR → GBP → USD) might yield a net positive return. Because these inefficiencies disappear in seconds, an automated system must scan the live network of prices to instantly find and exploit these risk-free profit loops.

**Optimization Method:** Network Flow Algorithms — specifically the Bellman-Ford Algorithm or Floyd-Warshall Algorithm. By transforming exchange rates into negative logarithms (-ln(rate)), the task of finding profitable arbitrage loops simplifies into detecting negative weight cycles in a directed graph.

**Validation Metrics:**

- **Execution Latency:** The time taken to find a cycle must be milliseconds or microseconds to beat market updates.
- **Transaction/Gas Fee Coverage:** Ensuring the calculated path return strictly exceeds the sum of network transaction fees and slippage.

---

## 3. Financial, Allocation & Scheduling Problems

### Mean Absolute Deviation (MAD) Portfolio Optimization

**Problem Description:** An investment manager wants to allocate capital across a diverse basket of financial assets (stocks, bonds, commodities). Instead of using standard variance to measure risk (which penalizes upside volatility equally with downside volatility), they want to minimize the Mean Absolute Deviation of the portfolio's historical returns, while ensuring a target minimum level of total return.

**Optimization Method:** Linear Programming (LP). Unlike Markowitz optimization (which requires Quadratic Programming for variance), MAD can be entirely linearized by introducing auxiliary variables for absolute deviations, allowing it to scale effortlessly to thousands of assets.

**Validation Metrics:**

- **Diversification Entropy / Herfindahl-Hirschman Index (HHI):** Ensures the LP solver hasn't heavily concentrated the portfolio into a single asset due to identical linear bounds.
- **Out-of-sample Sharpe and MAD Ratios:** Testing portfolio returns against historical holdout data.

---

### Workforce Shift Scheduling

**Problem Description:** A hospital, call center, or factory operates 24/7 and needs to schedule its staff. Demand fluctuates heavily by hour and day of the week. The organization must ensure it has enough employees with the right skills on shift at all times to meet operational demands, while strictly adhering to complex labor laws (e.g., maximum weekly hours, mandatory rest periods between shifts) and minimizing total labor costs.

**Optimization Method:** Mixed-Integer Linear Programming (MILP) with Column Generation (for large-scale rosters). It optimizes binary shift patterns against strict labor laws, preferences, and demand curves.

**Validation Metrics:**

- **Constraint Violations:** Zero tolerance for hard constraints (e.g., maximum consecutive working days or mandatory rest periods).
- **Labor Cost vs. Under-Staffing Penalty:** Validating that total shift cost balances well against the penalty costs of failing to meet base service demands.

---

### Electric Vehicle (EV) Recharging Strategy

**Problem Description:** A logistics company or individual driver is planning a long-distance road trip using an electric vehicle. Driving at higher speeds gets them to their destination faster but drains the battery much quicker. Charging a battery is non-linear (it takes much longer to charge from 80% to 100% than from 10% to 50%). The problem is to determine the optimal driving speeds and the exact locations and durations of charging stops to minimize total travel time.

**Optimization Method:** Mixed-Integer Linear Programming (MILP) mixed with Shortest Path Variants. The model maps out a trajectory where state-of-charge (SoC) is a continuous tracking variable, while stopping at a charging station is a binary decision variable.

**Validation Metrics:**

- **State of Charge (SoC) Lower Bound:** Ensuring the battery level mathematically never drops below 0% (or a safety buffer like 10%) at any continuous point along the timeline.
- **Total Travel Duration:** Validating that the time saved by driving faster outweighs the non-linear charging time curve at subsequent stops.

---

### Machine Scheduling & Job Shop Scheduling

**Problem Description:** A manufacturing facility must process a set of complex orders (jobs). Each job consists of multiple operations that must be performed in a strict sequential order on different shared machines. Only one job can be processed on a machine at a time. The objective is to sequence the jobs and allocate machine time to minimize the total time it takes to finish all jobs (makespan) and avoid idle bottleneck times.

**Optimization Method:** Constraint Programming (CP) or Asymmetric Mixed-Integer Linear Programming. CP excels here by using specialized interval variables and cumulative constraints to prevent two tasks from overlapping on the same machine.

**Validation Metrics:**

- **Makespan (C_max):** The total time elapsed from the start of the first job to the completion of the final job.
- **Machine Utilization Rate:** Checking for unnatural idle gaps in the schedule timeline to ensure the solver is truly minimizing bottlenecks.

---

### Facility Location Problem

**Problem Description:** A retail giant expanding its supply chain must decide where to construct new physical warehouses from a list of potential geographical sites. Opening a warehouse requires a heavy fixed investment cost. Once opened, shipping goods from that facility to local retail stores incurs a variable transportation cost. The company needs to choose the optimal subset of warehouses to open and map out which store is supplied by which warehouse to minimize the total combined cost of facility setups and shipping.

**Optimization Method:** Mixed-Integer Linear Programming (MILP). Binary variables dictate whether a facility is opened (y_j ∈ {0, 1}), while continuous variables (x_ij) dictate the fraction of customer demand supplied by that facility.

**Validation Metrics:**

- **Capacity Boundary Check:** Total demand routed to warehouse j must be strictly less than or equal to Capacity_j × y_j.
- **Supply-Demand Balance:** 100% of all customer nodes must have their demands met.
- **Marginal Cost Stabilization:** Verifying that adding one more facility increases fixed costs more than it saves in transportation costs.

---

## 4. Nonlinear & Convex Optimization

### Power Grid Economic Dispatch

**Problem Description:** A regional electricity grid operator must decide how much power each generator (coal, gas, nuclear, solar) should produce at every hour of the day to meet forecasted consumer demand at minimum total fuel cost. Each generator has a non-linear, convex cost curve — the marginal cost of producing an additional megawatt increases as the generator approaches its capacity limit. The operator must satisfy hard physical constraints: total supply must exactly equal total demand, transmission lines have thermal capacity limits, and voltage levels at each node must remain within safe bands. Violating any of these constraints risks blackouts or equipment damage.

**Optimization Method:** Second-Order Cone Programming (SOCP) or Semidefinite Programming (SDP) for the full AC Optimal Power Flow (OPF) formulation. The convex relaxation replaces the non-convex AC power flow equations with a tractable SOCP or SDP, provably finding the global optimum under mild conditions. For simpler DC approximations, Quadratic Programming (QP) suffices since generator cost curves are quadratic.

**Validation Metrics:**

- **Power Balance Residual:** Total generation minus total load plus transmission losses must equal zero (or within a tolerance of < 0.01% of total system load).
- **Constraint Violation Check:** Every transmission line flow must stay within its thermal rating; every bus voltage must remain within ±5% of nominal.
- **Duality Gap:** For the convex relaxation, a near-zero duality gap confirms the relaxation is tight and the solution is globally optimal, not just locally feasible.
- **Cost Reduction vs. Merit Order Dispatch:** The optimized dispatch cost compared to the naive merit-order baseline (simply running cheapest generators first, ignoring network constraints).

---

## 5. Multi-Objective Optimization / Pareto Frontier

### Sustainable Supply Chain Design

**Problem Description:** A global consumer goods company is redesigning its supply chain network — deciding which factories to operate, which distribution centers to open, and how to route goods from suppliers to end customers. Two objectives are in direct conflict: minimizing total logistics and operational cost (the traditional objective) and minimizing total carbon emissions across the entire network (driven by ESG commitments and regulatory pressure). Choosing the cheapest routes often means using high-emission freight modes (air cargo, diesel trucking) or operating older, less efficient factories. There is no single "best" solution — instead, there is a frontier of solutions representing every possible trade-off between cost and emissions, and the business must consciously choose where on that frontier it wants to operate.

**Optimization Method:** Multi-Objective Mixed-Integer Linear Programming solved via the Epsilon-Constraint Method (iterating over one objective while constraining the other to generate the full Pareto frontier) or the Weighted Sum Method (combining both objectives into a single scalar with varying weights). For large-scale instances, NSGA-II (Non-dominated Sorting Genetic Algorithm II) is applied as a metaheuristic to approximate the Pareto front efficiently without enumerating all integer solutions.

**Validation Metrics:**

- **Pareto Frontier Coverage:** The set of generated non-dominated solutions must span the full range from minimum-cost (ignoring emissions) to minimum-emissions (ignoring cost), with no large gaps in between.
- **Hypervolume Indicator:** Measures the volume of objective space dominated by the Pareto front relative to a reference point — a standard metric for comparing the quality of two Pareto approximations.
- **Marginal Abatement Cost (MAC) Curve:** The slope between adjacent Pareto points gives the cost (in dollars) of reducing one additional tonne of CO2 — this is the key business output that decision-makers use to select an operating point.
- **Dominated Solution Check:** Verify that no generated solution is strictly worse than another on both objectives simultaneously, which would indicate a solver or implementation error.

---

## 6. Queuing & Simulation-Based Optimization

### Emergency Room (ER) Staff and Bed Allocation

**Problem Description:** A hospital emergency room operates continuously with highly variable and unpredictable patient arrivals — surges during evenings, weekends, and flu seasons are common. Each patient follows a stochastic pathway: triage, examination, diagnostic tests, treatment, and either discharge or admission. The ER manager must decide how many nurses, doctors, and beds to allocate to each sub-unit (triage, resuscitation, fast-track) across different shifts. This cannot be solved with a closed-form equation because patient flow is a complex stochastic process — the interaction of random arrivals, variable service times, and shared resources creates non-linear congestion effects that only emerge through simulation.

**Optimization Method:** Simulation-Based Optimization combining Discrete-Event Simulation (DES) — built in SimPy or AnyLogic — as the objective function evaluator, with a metaheuristic search algorithm (Simulated Annealing, Genetic Algorithm, or Bayesian Optimization) driving the search over staffing configurations. Each candidate staffing plan is evaluated by running hundreds of simulation replications and averaging the resulting KPIs. Bayesian Optimization (using a Gaussian Process surrogate model) is particularly efficient here as it minimizes the number of expensive simulation runs needed.

**Validation Metrics:**

- **Average Patient Length of Stay (LOS):** The primary patient experience metric — the mean time from ER arrival to discharge or admission, averaged across simulation replications.
- **95th Percentile Wait Time:** Ensures the optimized staffing plan handles peak demand surges, not just average conditions.
- **Confidence Interval Width:** Each KPI estimate must have a sufficiently narrow 95% confidence interval across replications to confirm statistical reliability of the simulation output.
- **Staff Utilization Rate:** Ensures the solution doesn't achieve low wait times by massively overstaffing — utilization must stay within a practical operating band (e.g., 70–85%).
- **Simulation Variance vs. Optimization Noise:** Verifying that the performance difference between the best and second-best staffing configurations is statistically significant, not within simulation noise.

---

## 7. Integer Programming Classics

### Cloud Resource Bin Packing & Ad Slot Selection

**Problem Description (Bin Packing — Cloud Resource Allocation):** A cloud provider has a large pool of physical servers, each with fixed CPU and RAM capacity. Thousands of virtual machines (VMs) with varying resource requirements must be placed onto physical servers. The goal is to minimize the number of active physical servers (turning off unused servers saves energy and cost) while ensuring every VM's CPU and RAM requirements are satisfied and no server is overloaded. This is the multi-dimensional bin packing problem — each "bin" (server) has two capacity dimensions (CPU and RAM), and each "item" (VM) consumes both.

**Problem Description (Set Cover — Ad Slot Selection):** An online advertiser has a target audience defined by demographic segments (age groups, geographies, interest categories). A set of available ad placements each reaches a subset of these segments at a given cost. The advertiser must select the minimum-cost subset of ad placements that collectively covers every target demographic segment at least once.

**Optimization Method:** Mixed-Integer Linear Programming (MILP) for exact solutions on moderate instances. Binary decision variables y_j ∈ {0,1} indicate whether server j is active (bin packing) or ad slot j is purchased (set cover). For large-scale instances where exact MILP is too slow, LP Relaxation with Rounding provides fast approximate solutions with bounded approximation guarantees — the classical greedy set cover algorithm achieves a provable O(ln n) approximation ratio.

**Validation Metrics:**

- **Feasibility Check (Bin Packing):** Every VM must be assigned to exactly one server, and no server's total CPU or RAM allocation exceeds its physical capacity.
- **Coverage Check (Set Cover):** Every target demographic segment must appear in at least one selected ad placement — zero uncovered segments is a hard constraint.
- **Integrality Gap:** The ratio of the optimal integer solution to the LP relaxation bound, revealing how much is lost by the integrality requirement and how tight the LP bound is.
- **Approximation Ratio vs. Known Bounds:** For large instances solved with greedy or rounding heuristics, compare achieved cost against the theoretical lower bound to quantify solution quality.

---

## 8. Network Design & Flow

### Financial Settlement Network Optimization

**Problem Description:** In wholesale financial markets, thousands of bilateral payment obligations are created daily between banks — bank A owes bank B, B owes C, C owes D, and so on. If each obligation is settled individually, the gross volume of cash transfers is enormous, creating liquidity pressure on every institution. The settlement system operator wants to find the minimum set of actual cash transfers that nets out all obligations simultaneously, minimizing both the total value of transfers (liquidity cost) and the number of individual transactions (operational cost). This is a min-cost flow problem over a directed network where nodes are banks and edges are obligations.

**Optimization Method:** Min-Cost Flow (MCF) using the successive shortest path algorithm or network simplex method — both solve the LP relaxation of the flow problem exactly in polynomial time without requiring a general LP solver, making them orders of magnitude faster in practice. For the variant that also minimizes the number of transactions (a combinatorial objective), the problem extends to MILP with binary variables on each edge.

**Validation Metrics:**

- **Flow Conservation:** At every bank node, total inflow minus total outflow must equal that bank's net position (positive for net receivers, negative for net payers) — this is the fundamental feasibility condition.
- **Capacity Constraint Adherence:** No payment leg can exceed the bilateral credit limit agreed between the two counterparties.
- **Netting Efficiency Ratio:** (Gross obligation value − Optimized settlement value) / Gross obligation value. A ratio above 60–70% is typical in well-functioning multilateral netting systems.
- **Optimality Certificate:** The reduced costs on all non-basic flow edges must be non-negative (for minimization), confirming the network simplex solution is globally optimal.

---

## 9. Reinforcement Learning as Optimization

### Dynamic Pricing for Ride-Hailing / E-Commerce

**Problem Description:** A ride-hailing platform or e-commerce marketplace must set prices in real time across thousands of micro-markets simultaneously. Prices are not set once — they must be continuously adjusted based on the current system state: driver supply and rider demand levels in each zone, time of day, weather, local events, and competitor pricing. A high price reduces demand but attracts more supply; a low price fills demand but may create a supply shortage. The pricing agent must learn a policy — a mapping from observed system state to price — that maximizes long-run platform revenue or gross merchandise value, accounting for the delayed and non-linear effects of pricing decisions on future supply and demand dynamics.

**Optimization Method:** Deep Reinforcement Learning — specifically Proximal Policy Optimization (PPO) or Soft Actor-Critic (SAC) for continuous action spaces (since prices are continuous). The environment is either a learned simulator trained on historical pricing logs or a real A/B testing environment. The state space includes current supply-demand ratios by zone, time features, and recent price history. The reward signal is immediate revenue or a shaped reward that also penalizes excessive unfulfilled demand. For interpretability in production, the trained policy is often distilled into a simpler parametric form (e.g., a demand elasticity model) before deployment.

**Validation Metrics:**

- **Cumulative Reward (Return):** The discounted sum of rewards across an episode — the primary training signal. Must show consistent improvement across training iterations and stabilize at convergence.
- **Policy Gradient Variance:** High variance in gradient estimates causes unstable training. Monitoring explained variance of the value function baseline confirms the critic is learning useful state value estimates.
- **Offline Policy Evaluation (OPE):** Before live deployment, estimate the new policy's expected revenue using historical logged data via Inverse Propensity Scoring (IPS) or Doubly Robust estimators — provides a safe revenue estimate without running a live experiment.
- **A/B Test Revenue Lift:** The definitive production validation — the RL policy is rolled out to a treatment group and compared against the incumbent rule-based pricing policy on revenue per booking, fulfillment rate, and driver earnings fairness.
- **Supply-Demand Imbalance Rate:** Ensures the policy hasn't learned to maximize revenue by chronically under-supplying markets — a degenerate strategy that extracts short-term profit but erodes the platform's long-run health.
