# Probability Hit List — Driven by the Meta-Labeling Pipeline

*Two-week scope. Mapped against Lopez de Prado, Advances in Financial ML (AFML). The rule: learn only the probability your pipeline's next step demands. Cal Newport's "deep work on the thing that produces value," not probability-in-the-void.*

---

## The principle (read this first)

You are not "learning probability." You are building a meta-labeling pipeline that happens to require probability, and you're pulling the exact concepts forward as the code demands them. Meta-labeling (AFML Ch. 3.6) is a binary classifier that answers one question: **P(the primary model's bet is correct | features)**. Every topic below exists because some line of that pipeline breaks without it.

De-scope aggressively. Measure theory, sigma-algebras, characteristic functions, formal proofs — **skip entirely for now.** You need working fluency to build and validate, not a qualifying exam. Depth comes later, driven by the same JIT trigger.

---

## The map: topic → why the pipeline needs it → AFML chapter

| Probability topic | Where it bites in your pipeline | AFML chapter |
|---|---|---|
| Random variables, PMF/PDF/CDF | The triple-barrier label is a categorical RV (which barrier hit first) | Ch. 3.4–3.5 |
| Bernoulli / binomial | Meta-label is y ∈ {0,1}; base rate of profitable bets is a Bernoulli parameter | Ch. 3.6 |
| Conditional probability & Bayes | The meta-model *is* P(correct \| X). Precision/recall are conditional probabilities | Ch. 3.6 |
| Expectation & variance | Expected value of a bet; variance is what sizing and risk control | Ch. 3, Ch. 10, Ch. 15 |
| Confusion matrix → precision/recall/F1 | Meta-labeling's entire selling point is raising F1 by killing false positives | Ch. 3.6 |
| Independence & the IID assumption | Financial labels overlap in time → **not IID** → naive sampling is wrong | Ch. 4.1–4.3 |
| Sampling with/without replacement, bootstrap | Sequential bootstrap draws with adjusted probabilities to fix overlap | Ch. 4.4–4.5 |
| Law of large numbers & CLT | Why bagging works; why a Sharpe estimate has a sampling distribution | Ch. 6, Ch. 14 |
| Variance of the mean / bias–variance | The mathematical reason ensemble averaging reduces error | Ch. 6 |
| Prob → bet size (Gaussian CDF / z-score) | Converting the meta-model's probability into a position size | Ch. 10 |
| Sharpe ratio as an estimator (intro) | Bridge into statistics: deflated/probabilistic Sharpe, overfitting | Ch. 11, Ch. 14 |

---

## Week 1 — Foundations for labeling + meta-labeling

The goal by Friday: you can explain, in your own words, why the meta-model output is a conditional probability and why F1 is the metric that matters.

1. **Random variables — discrete vs. continuous, PMF/PDF/CDF.** Anchor it: the triple-barrier outcome is a discrete RV with 3 outcomes; a return is continuous.
2. **Expectation, variance, covariance.** These are the two moments everything downstream (sizing, risk, bagging) is built on.
3. **Conditional probability & Bayes' theorem.** The load-bearing concept. Meta-labeling = estimating P(y=1 | X). Understand how base rate distorts precision.
4. **Bernoulli & binomial distributions.** Your labels are Bernoulli trials; the count of wins over n bets is binomial.
5. **Confusion matrix → precision, recall, F1, Type I/II error.** Re-read AFML 3.6 *after* this — Lopez de Prado's whole argument is that meta-labeling trades recall for precision to lift F1.

**Week 1 build task:** implement or read through the triple-barrier labeling + meta-label generation (Ch. 3). Every time you hit a term you can't define probabilistically, that's your next study target.

---

## Week 2 — Sampling weights + why the model/validation works

The goal by Friday: you can explain why financial samples aren't IID, and why that breaks a naive train/test split.

6. **Independence & the IID assumption.** The single most important idea in AFML Ch. 4. Concurrent labels overlap → samples are dependent → standard ML assumptions fail.
7. **Bootstrap & sampling distributions.** Standard bootstrap assumes IID; sequential bootstrap (Ch. 4.5) adjusts draw probabilities to raise average uniqueness.
8. **Law of large numbers & CLT.** Why more (unique) samples stabilize estimates; why the Sharpe ratio itself is a random variable with a distribution.
9. **Variance of the mean / bias–variance decomposition.** The precise reason bagging (Ch. 6) reduces variance — averaging independent-ish estimators.
10. **Probability → bet size.** Lopez de Prado (Ch. 10) maps the meta-model's predicted probability to a position size via a Gaussian CDF / test-statistic transform. This is where probability output becomes a trading decision.
11. **(Bridge) Sharpe ratio as an estimator.** Not full statistics yet — just grasp that your backtest Sharpe is *one draw* from a distribution, which is why deflated/probabilistic Sharpe (Ch. 11, 14) exist. This is your on-ramp to the statistics phase.

**Week 2 build task:** implement average uniqueness + sample weights (Ch. 4) on your labeled data. Watch how it changes what "one training example" even means.

---

## Resources (spine, not a pile)

- **Blitzstein & Hwang, *Introduction to Probability* (Harvard Stat 110).** Free PDF + free full lecture series on YouTube. This is your one probability spine — don't collect five books. Topics 1–9 above map cleanly onto Stat 110's early lectures.
- **AFML itself** for the application layer. Read the relevant chapter *after* the matching probability topic, not before.
- **mlfinlab docs (Hudson & Thames)** for reference implementations of triple-barrier, meta-labeling, and sample weights — read the code alongside Ch. 3–4.

---

## What to explicitly NOT do

- Don't study statistics yet. It's the next phase; touching it now splits focus.
- Don't chase measure-theoretic rigor. Wrong tool for a builder at this stage.
- Don't read AFML front-to-back. You're pulling Ch. 3, 4, 6, 10, 14 — in that order, driven by the pipeline. The rest waits.
- Don't re-plan this list mid-sprint. Run it, hit the two build tasks, evaluate at the end of two weeks.
