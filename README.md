# sudoku-solver

Sudoku solver implementing DLX (Dancing Links + Algorithm X) by Donald Knuth.

## Output

![gif](./assets/sudoku.gif)

## Dancing Links

```
If A is empty, the problem is solved; terminate successfully.
Otherwise choose a column, c (deterministically).
Choose a row, r, such that A[r, c] = 1 (nondeterministically).
Include r in the partial solution.
For each j such that A[r, j] = 1,
    delete column j from matrix A;
    for each i such that A[i, j] = 1,
        delete row i from matrix A.
Repeat this algorithm recursively on the reduced matrix A.
```

## Pseudo-code for uncover

```
For each i = U[c], U[U[c]], . . . , while i != c
  for each j ← L[i], L[L[i]], . . . , while j != i
    set S[C[j]] ← S[C[j]] + 1
    and set U[D[j]] ← j, D[U[j]] ← j
Set L[R[c]] ← c and R[L[c]] ← c
```

## Pseudo-code for cover operation

```
Set L[R[c]] ← L[c] and R[L[c]] ← R[c]
For each i ← D[c], D[D[c]], . . . , while i != c
  for each j ← R[i], R[R[i]], . . . , while j != i
    set U[D[j]] ← U[j], D[U[j]] ← D[j]
    and set S[C[j]] ← S[C[j]] − 1
```

## Pseudo-code for search(k) operation

```
If R[h] = h, print the current solution (see below) and return.
Choose a column object c
Cover column c
For each r ← D[c], D[D[c]], . . . , while r != c
  set Ok ← r
  for each j ← R[r], R[R[r]], . . . , while j != r
    cover column j
    search(k + 1);
    set r ← Ok and c ← C[r];
  for each j ← L[r], L[L[r]], . . . , while j != r
    uncover column j
Uncover column c and return
```

# References

https://www.ocf.berkeley.edu/~jchu/publicportal/sudoku/0011047.pdf
https://www.kth.se/social/files/58861771f276547fe1dbf8d1/HLaestanderMHarrysson_dkand14.pdf

## Other usecases

We can use exact cover algorithmn to solve timetable planning too.

## Setup Typescript Testing

```
yarn add mocha @types/mocha chai @types/chai ts-node typescript --dev
```
