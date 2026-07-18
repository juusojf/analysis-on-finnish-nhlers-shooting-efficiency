# AI Workflow Documentation

This document describes my personal AI-assisted workflows used in this project. 
The workflows are documented as reusable patterns applicable to 
similar data analysis projects, not just this specific project.

### Workflow 1: Methodology design and pressure testing

**Use case:** Before writing any code, use AI to pressure-test 
analytical decisions and identify potential methodological weaknesses.

**How it works:**
1. Describe the research question and proposed methodology to AI
2. Ask: "What are the strongest counterarguments to this approach?"
3. Ask: "What methodological pitfalls should I be aware of?"
4. Incorporate valid concerns into the methodology before starting

**Example prompts:**
- "I'm planning to compare group-level shooting efficiency using 
  (goals - xG) / xG as my metric. What are the limitations of 
  this approach and what should I account for?"
- "What minimum sample size would be analytically defensible for 
  this type of group-level comparison?"

**Value added:** Catches methodological weaknesses before they 
become embedded in the analysis. Faster than literature review 
for established statistical concepts.

### Workflow 2: Code generation

**Use case:** Generate code and implement specific functions.

**How it works:**
1. Describe what the code needs to do
2. Specify input data structure and expected output
3. Iterate based on actual output

**Example prompts:**
- "Write a bootstrapping function that takes arrays of goals and 
  xG values and returns a 95% confidence interval for 
  (goals - xG) / xG"

**Value added:** Significantly speeds up implementation of 
well-defined functions / code. However, understanding the code remains critical as
AI might easily make mistakes that result in wrong results due to lack of context understanding or inaccurate prompting.

### Workflow 3: Documentation writing

**Use case:** Translate analytical decisions into clear written 
documentation for README and notebook md cells. 

**How it works:**
1. Describe the decision that was made and why
2. Ask AI to write documentation that explains both the what and the why
3. Review for accuracy as AI cannot know the context better than you
4. Edit to match your voice and correct any inaccuracies

**Important:** All analytical decisions in this project were made 
by the analyst. AI translated those decisions into documentation. 

**Value added:** Reduces the time spent on documentation without 
reducing its quality. Particularly useful for bulk writing and md-syntax.

### Workflow 4: Visualization Design

**Use case:** Generate publication-ready visualization code and 
iterate on design decisions.

**How it works:**
1. Describe what the visualization needs to communicate
2. Generate initial code and evaluate the output
3. Iterate with specific improvement requests

**Example prompts:**
- "The zero line represents NHL average, not zero efficiency. 
  How do I make this clearer in the chart?"
- "Add confidence interval whiskers to this horizontal bar chart 
  without making it look cluttered"

**Value added:** AI generates correct matplotlib syntax faster than documentation lookup. Design iteration 
is faster when you can describe changes in plain language. Author must make sure that the visualizations are
meaningful and and correct (=numbers are in line with the findings)

### Workflow 5: Analytical sanity checks

**Use case:** Before accepting a result, use AI to identify 
whether the finding makes sense and what alternative explanations exist.

**How it works:**
1. Share the finding with AI
2. Ask: "What could explain this result other than what I think?"
3. Ask: "Does this finding make sense given what we know about the domain?"
4. Design additional checks if alternative explanations are plausible

**Example from this project:**
All nationalities showed negative efficiency in the slot zone. 
Before concluding this was a real finding, AI identified that 
MoneyPuck's xG model was trained on older data and may 
systematically overestimate slot shot probabilities. Also our own zone 
classifications likely factored as they are not made to be in line with
MoneyPuck's xG-model. This led  to normalizing results to NHL average 
rather than using absolute xG values.

**Value added:** Reduces confirmation bias. Ensures findings 
are robust before being reported as conclusions.

## Reflection

The most valuable AI contributions in this project were 
bulk code generation and analytical dialogue. Having a discussion 
partner to pressure-test ideas, identify blind spots, and 
structure investigations ensured a smooth project. Code generation 
saved time but could have been done without AI. 

The key limitation: AI cannot validate findings against reality. 
Every output requires human judgment to assess whether it makes 
sense in the specific domain context.