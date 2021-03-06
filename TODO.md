# issues

xylo / xylica?

## impl

hand-craft genomes to test each operation.

use a simple testing physics/world.

## design

internal dynamics (GRN) should have negatives -- repressors -- as well as positive TFs


what is the main loop for a cell?
  - reacting to new external stimulus only?
    - though including results of our own actions: reproduction / forces / sugar channels
  - what about internal dynamics?
    - with GRN, input/output seemed awkward
    - with stringmol matching, i/o is natural but no internal dynamics.
    - delay-goto - carry over a reaction to next time step
      - but vs new stimuli? and what about infinite loops.
    - product - accumulates *inside* cell and *competes* to react.
      - also decays.
      - produce up to a max level of each, and have a max number of different TFs.
      - i.e. GRN-like.
      - then epigenetic silencing could be limited to (and mandatory for) reproduction
        - tissue specialisation

*********
alignment should be stochastic based on match score
and considering all candidate alignment locations.
*********

matching should include a monotonic function of alphabetical distance per base
  - as a continuous selection signal
  - alternatively: reduce alphabet to ~4 bases and interpret codons as operations.
    - correspondingly increase match score threshold.

(def op-names
  '[end
    form-bond
    break-bond
    clone
    sex
    about-face
    rot-left
    rot-right
    sugar-start
    sugar-stop
    push
    silence
    unsilence
    product
    energy-test
    goto
    reference
    ])

17 ops.
codons of 2 in alphabet of 5 = 25 so roughly half are coding.
alternatively codons of 3 in alphabet of 4 = 64.
codons of 3 in alphabet of 3 = 27.

is binding/unbinding once per stimulus?
  - if created touching rock, only react once?
  - or do we re-evaluate if a conditional changes / or epigenetic state changes?
    - fine if the reactions are idempotent
      - but they are not: reproduction / push / silence

all reactions should by default have a persistent effect

so, cell consists of genome + epigenetic marks + TFs
  - stimuli and TFs compete to react each step
    - with probability according to goodness of match.
  - TFs decay at some rate

how does unbinding react anyway?
  - reverse sequence for alignment?

once a sugar channel is opened, does it
  - pass sugar every step (until threshold?)
  - react every step to query

energy-test conditional
  - threshold is calculated from position in genome from 0 to max energy level

limit instructions per step
  - at most one copy per step.
  - children can not copy in first step. (anyway: energy cost)

energy cost of reactions - esp clone


matching to self clone:
  - match to complement is symmetric so two equally good candidate binds on each side
  - use first in sequence to look up reactions
  - need specialisation to be interesting
    - is silencing enough?
    - execution forks at copy time.
      - run through parent first. when that ends, child begins?
      - or, child could be anti-sense?
    - want/expect silencing in parent and/or child.
      - make this the default behaviour - always silence by reading next templates
        - read begin token up to next opcode (any). then end token up to following opcode.
        - child uses following two templates, similarly.
      - unsilencing?
        - a normal action
    - additional specialisation mechanism:
      - initialise new cell with special birth products


also: GRN-like products are transcribed from a template in DNA
  - product will just match its original template
  - so need translation
  - if in complement, the template will match binding site in a clone cell
  - so need translation different to cell-cell matching (not complement)

silencing
  - continue to best match template alignment
  - wrap around?
    - or only consider downstream genome
    - or use current direction (fwd/back)
  - if no match (0), no-op

unsilencing
  - match to silenced bases of genome?

sexual reproduction - align genomes at crossover points (use trace)

## future

water
