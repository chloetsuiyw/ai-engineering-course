# AI Use Case Canvas

## Business process
Match employees to training opportunities (P005 — HR learning & development)

**Current pain point:** L&D teams manually match employees to courses based on role profiles and manager input. This is time-consuming, inconsistent, and often misses skill gaps that employees themselves have flagged in surveys but that managers are unaware of.

## Data inputs
- Role profiles (job family, level, required competencies)
- Skill survey responses (self-assessed gaps and interests)
- Course catalogue (topic, format, duration, prerequisites)
- Career interest forms (employee-stated development goals)
- Past course completion records (what was taken, completion rate, ratings)

## Model approach
**Both predictive ML and GenAI.**

- **Predictive ML:** Recommend courses based on skill gaps and historical completion patterns. The model ranks catalogue items by relevance to each employee's profile and gap data.
- **GenAI:** Generate a personalised learning plan draft that explains why each course was suggested and how it connects to the employee's stated career goals.

The two approaches need separate evaluation methods — the ML ranking is evaluated quantitatively, the GenAI output is evaluated qualitatively by L&D reviewers.

## Interface
HR portal recommendation widget. Employees see a ranked list of suggested courses with a short plain-English rationale. Managers see a team-level skill-gap summary to support 1:1 conversations. L&D staff see a review queue for generated learning plans before they are shared.

## Evaluation
- **Click-through and course completion rate** — primary business KPI; did employees actually take the recommended courses?
- **Human review of generated learning plans** — L&D staff rate each draft on relevance, tone, and accuracy before release.
- **Employee satisfaction survey** — short pulse after each recommendation cycle asking whether suggestions felt relevant and useful.
- Measured over 2–3 performance review cycles to allow enough time for completion data to accumulate.

## Deployment
1. **Notebook prototype** — validate the recommendation logic on historical data; check for obvious bias before touching live employees.
2. **Internal pilot** — small volunteer group (one team or department); collect completion and satisfaction data.
3. **HR portal integration** — embed the widget once pilot results are satisfactory; L&D review queue active from day one.
4. **Impact monitoring** — track KPIs each review cycle; retrain or adjust the model if recommendation quality drifts.

## Governance
**Risk:** The model may recommend fewer development opportunities to employees in certain roles, tenures, or demographic groups if historical completion patterns reflect existing workplace inequalities — effectively automating and amplifying existing bias.

**Mitigation:** Audit recommendations by role, department, gender, and tenure before any pilot launch. Flag statistically significant gaps for human review. Require L&D sign-off on all generated learning plans. Ensure employees can see why a course was recommended and can override or dismiss suggestions without penalty. Obtain explicit consent before using skill survey data for automated recommendations.
