# ASSIGNMENT: Sampling and Reproducibility in Python

Read the blog post [Contact tracing can give a biased sample of COVID-19 cases](https://andrewwhitby.com/2020/11/24/contact-tracing-biased/) by Andrew Whitby to understand the context and motivation behind the simulation model we will be examining.

Examine the code in `whitby_covid_tracing.py`. Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

Modify the number of repetitions in the simulation to 100 (from the original 1000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times

# Author: Yitong Zhao

```
1. The first sampling is about the random number of people getting infected (i.e., np.random.choice(ppl.index, size=int(len(ppl) * ATTACK_RATE), replace=False)

Sample Size is the rate of infection (10%, ATTACK_RATE) multiplied by the number of all people. Sample frame is the entire dataset (with 200 people attending weddings and 800 attending brunches).

Because each person was randomly selected, the sampling approach was simple random. As described in the blog post, this is simliar to the process of how an outbreak might spreadh within a larger group, with only subsets of people who attend those events getting infected.

2. The second sample is the random number of people getting traced, whether they were infected or not. (i.e., np.random.rand(sum(ppl['infected'])) < TRACE_SUCCESS)

Sample Size is the rate of successful tracing (20%, TRACE_SUCCESS) multiplied by the number of people who got affected, so the sample size is 20% multiplied by the number of people infected.

Sampling Frame is all infected individuals. Because each infected person is either marked as traced (0) or not (1), each outcome has an equal possiblity. It was an uniform distribution.

This reflects the biases of tracing mentioned in the blog post, given that not all people who are infected will be traced successfully.


The plot I got from running the python code is similar to the plot in the blog post (i.e., true proportion smaller than observed proportions), but with a much smaller difference between the true proportion and the observed proportion. The plot I got had a less than .10 difference while the blog post showed a ~.40 difference.


After modifying the number of simulations from 1000 to 100, the observed proportions' distribution (i.e., "traced to weddings" bars) is shifting around the true proportions' distribution ("infections from weddings"). The reproducibility of the results largely decreased given the instability/variance in the results I am getting with a much smaller number of simulations.


To make the results reproducible, I have set a random seed by adding "np.random.seed(123)" in my code.

```


## Criteria

|Criteria|Complete|Incomplete|
|--------|----|----|
|Altercation of the code|The code changes made, made it reproducible.|The code is still not reproducible.|
|Description of changes|The author explained the reasonings for the changes made well.|The author did not explain the reasonings for the changes made well.|

## Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `23:59 - 09/04/2025`
* The branch name for your repo should be: `assignment-1`
* What to submit for this assignment:
    * This markdown file (a1_sampling_and_reproducibility.md) should be populated.
    * The `whitby_covid_tracing.py` should be changed.
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sampling/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [ ] Create a branch called `assignment-1`.
- [ ] Ensure that the repository is public.
- [ ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via the help channel in Slack. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
