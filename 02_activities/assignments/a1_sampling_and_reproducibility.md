# ASSIGNMENT: Sampling and Reproducibility in Python

Read the blog post [Contact tracing can give a biased sample of COVID-19 cases](https://andrewwhitby.com/2020/11/24/contact-tracing-biased/) by Andrew Whitby to understand the context and motivation behind the simulation model we will be examining.

Examine the code in `whitby_covid_tracing.py`. Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

Modify the number of repetitions in the simulation to 1000 (from the original 50000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times

# Author: Omar Khan

```
Please write your explanation here...

1. Initial Population Sampling:
Function: simulate_event(m)
Procedure: Creates a population of 1,000 individuals, with 200 attending weddings and 800 attending brunches.
Sample Size: 1,000 individuals.
Sampling Frame: Attendees of weddings and brunches.
2. Infection Sampling:
Function: simulate_event(m)
Procedure: A random 10% subset (100 individuals) of the population is infected, based on the ATTACK_RATE (10%).
Sample Size: 100 individuals.
Underlying Distribution: Binomial distribution (10% chance of infection for each individual).
3. Primary Contact Tracing:
Function: simulate_event(m)
Procedure: A 20% subset of infected individuals is traced based on the TRACE_SUCCESS rate.
Sample Size: 20% of infected individuals (approximately 20).
Underlying Distribution: Binomial distribution (20% chance of being traced).
4. Secondary Contact Tracing:
Function: simulate_event(m)
Procedure: If more than 2 traced individuals are at an event, all infected attendees at that event are traced.
Sample Size: Variable, depending on traced individuals exceeding the threshold.
Underlying Distribution: Conditional on primary tracing; no fixed distribution.
Relation to the Blog Post:
Whitby’s blog highlights the bias in contact tracing, as certain events (e.g., weddings) are more easily traced than others (e.g., private gatherings). The simulation mirrors this by over-representing certain events in the traceable sample, reflecting real-world biases in contact tracing. This bias distorts the perceived infection sources, just as discussed in the blog.

Reproducing the Graphs from the Blog Post
Original Graph Comparison:
The script partially reproduces the blog’s graph, but with key differences:

Blog Post Graph: Shows a "True proportion" tightly clustered around 0.2, while the "Observed proportion" spreads from 0.2 to 0.6, indicating significant bias in the observed data.
Code Output: The observed proportions are tightly clustered around 0.15–0.25, with minimal spread, suggesting that the observed data closely matches the true data, implying less bias than shown in the blog.
The difference could stem from variations in simulation parameters or random factors in the code.

Reproducibility with 1,000 Repetitions
When reducing repetitions from 50,000 to 1,000:

Consistent Shape: The histograms maintain consistent central tendencies, with peaks around 0.15–0.25 for both "Traced to Weddings" and "Infections from Weddings."
Increased Variability: Although the central trends are consistent, the specific shapes and peaks of the histograms vary due to fewer repetitions, which increases the sample variability.
Without a fixed random seed, results can fluctuate more with fewer repetitions. Increasing the number of repetitions reduces variability, leading to more stable results.

Making the Code Reproducible
To ensure reproducibility, the following changes were made:

Global Random Seed:
Added np.random.seed(10) at the beginning to control random processes (e.g., infection and tracing) and ensure consistent results across runs.
Parameterized Repetitions:
The number of repetitions (num_repetitions) is now passed to the run_simulation_and_plot() function, making it easier to adjust the number of simulations without altering the code logic.
These changes ensure that the simulation produces identical results each time it is run, making the script reproducible.


## Criteria

|Criteria|Complete|Incomplete|
|--------|----|----|
|Altercation of the code|The code changes made, made it reproducible.|The code is still not reproducible.|
|Description of changes|The author explained the reasonings for the changes made well.|The author did not explain the reasonings for the changes made well.|

## Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `HH:MM AM/PM - DD/MM/YYYY`
* The branch name for your repo should be: `sampling-and-reproducibility`
* What to submit for this assignment:
    * This markdown file (sampling_and_reproducibility.md) should be populated.
    * The `whitby_covid_tracing.py` should be changed.
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sampling/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [ ] Create a branch called `sampling-and-reproducibility`.
- [ ] Ensure that the repository is public.
- [ ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via our Slack at `#cohort-3-help`. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
