---
title: "Finite State Network"
date: 2019-03-25T17:23:06-05:00
---

### Finite-State Network 有限狀態機
有限狀態機在詞法學上的應用：
- Finite-state Tokenizer
- Finite-state morphological analyzer/generators(Lexical Transducer)
- Finite-state post of speech tagger
- Finite-state shallow syntactic parser

- so called : **Finite-State Automaton** (plural automata)
- It consists of **states** and **arcs**, has a single designed **start state** and any number (zero or more) **final state**
- Final state is the accepting state.

![img1](/FSA.png)
- O is the start state
- 25 is the end state (double circle)


### Symbols / Alphabet / Words / Language

- **Symbol:** The input to the machine ("0","25" from image 1)
- **Alphabet:** The set of valid symbols that the machine will accept
- **Words:** The sequence of symbols that the machine will accept
- **Language:** The entire set of words that the machine accepts or recognizes 

**regular language**: language that FSA can recognize / can be represented by regular expression
**regular expression**: a sequence of characters that define a search pattern
epsilon symbol: the empty string, transition without any symbol being consumed

<!--more-->
### Actions of FSA

#### Analysis & Generation
- analysis: look up, symbol matching. The (surface form)lower form to the upper(underlying form).
- generate: use analysis string(upper) to generate surface strings(lower)
 
#### Transition & Consume
- (0 &rarr; 25)
- transition: the network machine moves to the new state 
- 0 is consumed

### Finite State Transducer
- a **transducer** is a device that converts energy from one form to another
- microphone is a transducer that converts physical vibrations of air into analogous electrical signals
- upper side: input
- lower side: output
- Looks similar to FSA, except it has upper side and lower side.
- usually looks like ?:? (? means any symbol, : is mapping)


### Tools:
- [foma](https://github.com/mhulden/foma/blob/master/foma/docs/simpleintro.md): to do computational morphology
- [dot/graphviz](http://www.graphviz.org/): to draw finite state machine
- [foma regular expression](http://foma.sourceforge.net/dokuwiki/doku.php?id=wiki:regexreference)