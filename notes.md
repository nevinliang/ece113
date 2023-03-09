# ch 4

relaxed system: output seq is 0 if input seq is 0
- if x(n) = 0 for n < n0 then y(n) = 0 for n < n0
- ex of relaxed system: y(n) = x(n - 1)
- ex of non-relaxed system: y(n) = x(n + 1)

dynamic system: system with memory
- ex: y(n) = x(n - 1)
    - depends on previous values of x

time invariant systems: delay in input yields delay in output
- ex: y(n - K) = S[x(n - K)]
- y(n) = y(n - 1) + x(n)

causal systems: output depends on present and past examples of input sequence
- ex: y(n) = nx(n - 1)

stable systems: BIBO stable = bounded input yields bounded output
- ex: y(n) = x(n^2)
- !ex: y(n) = nx(n)
    - because what if x(n) is cosine -> y(n) grows without bound

linear systems: satisfies superposition
- S[a1x1(n) + a2x2(n)] = a1y1(n) + a2y2(n)

