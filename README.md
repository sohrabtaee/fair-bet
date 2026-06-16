# Bet Calculator

A simple calculator for determining how much each person should contribute to a bet based on their confidence in the outcome.

## The Idea

Two people disagree about whether an event will happen.

Examples:

- Person 1: 60% chance it happens
- Person 2: 20% chance it happens

One person must be above 50% and the other below 50%.

The calculator converts their probabilities into a stake split.

The core principle is:

> The more confident you are, the more money you should risk if you are wrong.

## How It Works

Given:

- Person 1 probability: `p1`
- Person 2 probability: `p2`

We normalize the probabilities so they add up to 100%.

### Formula

```text
normalizedP1 = p1 / (p1 + p2)
normalizedP2 = p2 / (p1 + p2)
```

The total bet amount is then split according to these normalized values.

```text
stakeP1 = totalBet × normalizedP1
stakeP2 = totalBet × normalizedP2
```

## Example

Input:

```text
Person 1: 60%
Person 2: 20%
Total Bet: $100
```

Normalization:

```text
60 / (60 + 20) = 75%
20 / (60 + 20) = 25%
```

Result:

```text
Person 1 contributes $75
Person 2 contributes $25
```

### Outcomes

If the event happens:

```text
Person 1 wins
Profit: $25
```

If the event does not happen:

```text
Person 2 wins
Profit: $75
```

## Why This Approach?

This calculator treats the submitted percentages as measures of confidence.

A person who claims:

```text
90%
```

is considered more confident than someone claiming:

```text
60%
```

Therefore they:

- Risk more money
- Receive a smaller reward if correct
- Suffer a larger loss if wrong

This mirrors the intuition that stronger confidence should come with greater accountability.

## Validation Rules

The calculator rejects bets where:

### Both people believe the event is likely

```text
60% vs 70%
```

### Both people believe the event is unlikely

```text
20% vs 40%
```

### Either probability is exactly 50%

```text
50% vs 20%
```

### Probabilities are outside the range

```text
0%
100%
negative values
```

The calculator is designed only for situations where the two participants are taking opposite sides of the same prediction.

## Notes

This system intentionally focuses on relative confidence.

Examples:

```text
60% vs 20%
```

and

```text
90% vs 30%
```

both normalize to:

```text
75% vs 25%
```

because the ratio between the predictions is the same.

The goal is not to estimate the true probability of the event.

The goal is to determine a stake split that reflects the participants' relative confidence levels.
