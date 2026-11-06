# SF Ballot-O-Matic

An interactive page for looking at how San Francisco ballots voted in the November 3, 2026
Consolidated General Election, built from the cast vote record. It has three tabs:

- **Crosstabs:** compare how the same ballots voted on two contests. For example: of the
  ballots that voted no on Measure G, how many voted yes on Measure H?
- **Voter guides:** how many voters followed each of 11 voter guides exactly or nearly so,
  which guide each voter matched best, and where voters broke with each guide.
- **Voter clusters:** k-means groups of voters who voted alike, how each group voted, where
  each group lives, and which guides each group followed.
- **Coalition builder:** pick any combination of choices and see how many mail voters made all
  of them, which neighborhoods they live in, and how they voted on everything else.

**Live site:** https://zachlipton.github.io/sf-ballotomatic/

## How it works

The page is built from the Department of Elections' cast vote record (CVR) export. Each
ballot is printed on four cards, and the CVR records each card separately. Everything is
precomputed and embedded in `index.html`; there is no server.

- Contests on the same card are compared using every ballot.
- Contests on different cards, and the whole-ballot voter guide and cluster tabs, use mail
  ballots only: to protect voter privacy, Election Day in-person ballots can't be analyzed
  this way. A few percent of mail ballots are excluded due to data quality issues, and a
  small share (about 0.3%) are estimated to be affected by error.

- Ranked-choice contests show first choices.
- Write-ins count as undervotes.
- In races where voters can pick more than one candidate, percentages are shares of
  ballots and can add up to more than 100%.
- Voter guides and clusters leave out judicial retentions and uncontested races. Skipped
  contests don't count for or against a voter, but ballots that skipped more than a quarter
  of the contests in question aren't compared or grouped.
- Endorsements come from the [SF Voter Guide Comparison](https://lizziesiegle.com/sf-voter-guides/)
  (compiled from [SF Endorsements](https://sfendorsements.com/) and the guides' own pages),
  with the SF Chronicle's checked against its published endorsements.

- The coalition builder loads ballot-level mail data (`coalition.bin`) located only to one of
  SF's analysis neighborhoods; ballots in small neighborhood groups carry no location, and
  results are shown only for coalitions of at least 100 ballots.

Results are preliminary and change as more ballots are counted. The page shows the
report and the time of the CVR export it was built from.
