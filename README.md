# Runoff Voting System

This program simulates a runoff election, where voters rank candidates in order of preference. If no candidate wins a majority, the candidate with the fewest votes is eliminated and their votes are redistributed, continuing until a candidate has a majority.

## Usage

To compile the program:

```sh
gcc runoff.c -o runoff -lcs50
```

To run the program:

```sh
./runoff [candidate ...]
```

For example, to run an election with three candidates Alice, Bob, and Charlie:

```sh
./runoff Alice Bob Charlie
```

## Features

- **Vote Recording**: Allows voters to rank candidates in order of preference.
- **Runoff Process**: Automatically eliminates the candidate with the fewest votes and redistributes those votes until a candidate wins a majority.
- **Tie Handling**: Detects ties and announces all tied candidates as winners if no clear winner can be determined.

## Code Overview

### Data Structures

- **Candidate**: Each candidate has a `name`, `votes`, and `eliminated` status.
- **Preferences**: A 2D array `preferences[i][j]` stores the j-th preference of voter i.

### Constants

- `MAX_VOTERS`: Maximum number of voters (100).
- `MAX_CANDIDATES`: Maximum number of candidates (9).

### Global Variables

- `candidates`: Array of `candidate` structs.
- `voter_count`: Number of voters.
- `candidate_count`: Number of candidates.

### Functions

- **`bool vote(int voter, int rank, string name)`**: Records a voter's preference.
- **`void tabulate(void)`**: Counts votes for non-eliminated candidates.
- **`bool print_winner(void)`**: Checks and prints the winner if one exists.
- **`int find_min(void)`**: Finds the minimum number of votes any remaining candidate has.
- **`bool is_tie(int min)`**: Checks if the election is tied.
- **`void eliminate(int min)`**: Eliminates the candidate(s) with the fewest votes.

### Main Function

1. **Input Validation**: Ensures correct usage and initializes candidates.
2. **Vote Collection**: Collects voters' preferences.
3. **Runoff Process**: Repeatedly tabulates votes, checks for a winner, eliminates the candidate with the fewest votes, and handles ties.

### Detailed Function Descriptions

#### `bool vote(int voter, int rank, string name)`
- Records a valid vote by checking the candidate's name and updating the preferences array.

#### `void tabulate(void)`
- Counts votes for each non-eliminated candidate based on voters' preferences.

#### `bool print_winner(void)`
- Checks if any candidate has a majority of the votes and prints the winner's name.

#### `int find_min(void)`
- Finds and returns the smallest number of votes that any non-eliminated candidate has.

#### `bool is_tie(int min)`
- Determines if all remaining candidates have the same number of votes, indicating a tie.

#### `void eliminate(int min)`
- Eliminates all candidates who have the minimum number of votes.

## Example

Suppose we have 3 candidates: Alice, Bob, and Charlie, and 5 voters. Here is how the election might proceed:

1. **Initial Votes**:
    - Voter 1: Alice > Bob > Charlie
    - Voter 2: Bob > Charlie > Alice
    - Voter 3: Charlie > Alice > Bob
    - Voter 4: Alice > Charlie > Bob
    - Voter 5: Bob > Alice > Charlie

2. **Tabulate Votes**:
    - Alice: 2
    - Bob: 2
    - Charlie: 1

3. **Eliminate**: Charlie is eliminated.

4. **Redistribute Votes**:
    - Voters who preferred Charlie now contribute their votes to their next choice.

5. **Repeat** until a candidate has a majority.

