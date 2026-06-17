# Fair Bet Calculator

A single-page calculator for splitting a bet fairly based on each person's confidence in the outcome.

Every bet must include a settlement date, because a prediction without a deadline cannot be resolved.

## What It Does

The app asks for:

- A bet description
- Each person's name
- Each person's probability estimate
- The total bet amount
- A settlement date

It then calculates:

- How much each person should contribute
- Who wins if the event happens or does not happen
- The normalized confidence split

The result box also includes a `Share calculation` button that uses the device/browser native share sheet when supported.

## Core Idea

Two people disagree about whether an event will happen.

Example:

```text
Ava: 60% chance it happens
Rob: 20% chance it happens
Total bet: €100
Settlement date: June 30, 2026
```

One person must be above 50% and the other below 50%.

The calculator converts their probabilities into a stake split.

The core principle is:

> The more confident you are, the more money you should risk if you are wrong.

## How It Works

Given:

- Person 1 probability: `p1`
- Person 2 probability: `p2`
- Total bet amount: `totalBet`

The probabilities are normalized so they add up to 100%.

```text
normalizedP1 = p1 / (p1 + p2)
normalizedP2 = p2 / (p1 + p2)
```

The total bet amount is split according to those normalized values.

```text
stakeP1 = totalBet × normalizedP1
stakeP2 = totalBet × normalizedP2
```

## Example

Input:

```text
Ava: 60%
Rob: 20%
Total bet: €100
Settlement date: June 30, 2026
```

Normalization:

```text
60 / (60 + 20) = 75%
20 / (60 + 20) = 25%
```

Result:

```text
Ava should put in: €75.00
Rob should put in: €25.00
```

If the event happens:

```text
Ava is right and wins Rob's €25.00.
```

If the event does not happen:

```text
Rob is right and wins Ava's €75.00.
```

## Validation Rules

The calculator rejects bets where:

- The bet description is empty
- The settlement date is empty
- The settlement date is in the past
- The total bet amount is `0`, negative, or missing
- Either probability is `0`, `100`, negative, or missing
- Either probability is exactly `50`
- Both people are above `50%`
- Both people are below `50%`

The calculator is designed only for situations where the two participants are taking opposite sides of the same prediction.

## Sharing

After calculation, the result can be shared with the `Share calculation` button.

This uses the browser's native Web Share API. It works only in browsers/devices that expose `navigator.share`.

## Notes

This system intentionally focuses on relative confidence.

These inputs:

```text
60% vs 20%
```

and:

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
