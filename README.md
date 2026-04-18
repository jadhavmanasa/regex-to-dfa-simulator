# regex-to-dfa-simulator
Regex → NFA → DFA → Minimized DFA Simulator with visualization

## Theory of Computation — Class Participation Submission

A complete simulation of the full automata conversion pipeline using only HTML, CSS, and JavaScript. No libraries or frameworks required.
## Features

### Step 1: Regex → NFA (Thompson's Construction)
- Parses the regular expression into an AST (Abstract Syntax Tree)
- Applies Thompson's construction rules recursively:
  - Literals → 2-state NFA with one labelled transition
  - Concatenation → connect via ε-transition
  - Union (A|B) → new start/end with 4 ε-transitions
  - Kleene star (A*) → new start/end with 3 ε-transitions
  - Plus (A+) → A concatenated with A*
  - Optional (A?) → union with ε
- Displays NFA state diagram (SVG)
- Shows full transition table including ε-transitions
- Computes and displays all ε-closures

### Step 2: NFA → DFA (Subset Construction)
- Computes ε-closure of start state
- Iteratively applies move() and ε-closure() for each symbol
- Each DFA state = a set of NFA states
- A DFA state is accepting iff it contains the NFA accept state
- Displays DFA state diagram (SVG)
- Shows full transition table
- Execution log of every ε-closure and move computation

### Step 3: DFA → Minimized DFA (Table-Filling Algorithm)
- Initializes table: mark all (accept, non-accept) pairs as distinguishable
- Iterates: mark (p,q) if δ(p,a) and δ(q,a) are already distinguished
- Repeats until no new marks
- Merges indistinguishable state pairs into equivalence classes
- Displays minimized DFA diagram (SVG)
- Shows the complete distinguishability table (✗ = distinguishable, ~ = equivalent)
- Lists all equivalence classes and which states merged

### Step 4: Summary
- Side-by-side comparison of state counts at each stage
- Explains each algorithm with formal definitions
- States the Myhill–Nerode minimality guarantee

### Bonus: String Testing
- Test any string against the minimized DFA
- Instant accept / reject result

---

## Supported Regex Syntax

| Syntax | Meaning       |
|--------|---------------|
| `a-z`  | Literals      |
| `0-9`  | Digits        |
| `\|`   | Union / OR    |
| `*`    | Kleene star   |
| `+`    | One or more   |
| `?`    | Zero or one   |
| `()`   | Grouping      |
| `ε` / `eps` | Epsilon  |

---

## Concepts Covered (from syllabus)

- **Unit 1**: DFA, NFA, ε-transitions, NFA→DFA equivalence, DFA minimization
- **Unit 2**: Regular expressions, relation between RE and FA (RE→NFA→DFA)

---

## Example Inputs

| Regex | Language |
|-------|----------|
| `(a\|b)*abb` | Strings ending in "abb" |
| `a(a\|b)*b` | Strings starting with a, ending with b |
| `ab*\|ba*` | a followed by b's, or b followed by a's |
| `a*b*` | Zero or more a's followed by zero or more b's |
| `(a\|b)*a(a\|b)` | Strings where second-to-last char is a |

---

All logic is self-contained in `index.html`. The application runs entirely client-side with no external dependencies.
