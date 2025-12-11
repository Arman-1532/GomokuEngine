# Gomoku Engine

Playable Gomoku (Five in a Row) engine with a CLI and Tkinter GUI. The engine
implements iterative-deepening minimax with alpha-beta pruning and a lightweight
pattern-based evaluator, so you can play against the AI, run human vs human
simulations, or explore move generation on a fixed size board(14 X 14).

## Features
- Search: iterative-deepening minimax with alpha-beta pruning and move ordering.
- Heuristics: pattern-scoring evaluator that prefers open fours, threes, and
  immediate wins.
- Interfaces: text-based CLI plus a fullscreen Tkinter GUI with optional AI vs.
  AI simulation mode.
- Configurable: board size, search depth, time per move, cell size (GUI), and
  simulator delay are all tunable via flags.
- Tested core: board logic, evaluation, and engine move selection covered by
  simple regression tests.

## Project Structure
- `src/board.py`: immutable-ish board representation, win detection, and move
  generation near existing stones.
- `src/evaluation.py`: heuristic pattern evaluator for scoring positions.
- `src/search.py`: minimax with alpha-beta pruning and iterative deepening.
- `src/engine.py`: engine wrapper that selects moves within depth/time limits.
- `src/ui_cli.py`: command-line interface to play vs. the AI.
- `src/ui_gui.py`: Tkinter-based GUI with human-vs-AI, human-vs-human, and
  AI-vs-AI simulation modes.
- `tests/test_board.py`: sanity checks for win detection, evaluation, and engine
  move selection.

## Getting Started
Requirements:
- Python 3.10+ (standard library only; Tkinter is included with most Python
  distributions on macOS/Linux).

Setup:
1) (Optional) Create a virtual environment:
   ```bash
   python -m venv .venv
   source .venv/bin/activate
   ```
2) Install/verify Tkinter if it is missing on your platform.

## Running the Game
CLI (play as black; enter moves as `row col`):
```bash
python -m src.ui_cli --size 15 --depth 4 --time 2.0
```

GUI (fullscreen window):
```bash
python -m src.ui_gui --size 15 --cell 48 --depth 3 --time 2.0
```
- Start screen lets you choose Human vs Human or Human vs AI.

## Configuration Flags
- `--size`: board dimension (default 14).
- `--depth`: maximum search depth.
- `--time`: time limit per AI move in seconds (used to stop iterative deepening).
- GUI only: `--cell` (pixel size per cell), `--simulate` (AI vs AI mode),
  `--delay` (ms between simulator moves).

## How It Works
- Board: integer grid (1 = black, -1 = white, 0 = empty) with neighbor-based
  move generation to keep branching small.
- Evaluation: scans rows, columns, and diagonals for scoring patterns (open
  fours, threes, fives, etc.), balancing own and opponent threats.
- Search: iterative-deepening minimax with alpha-beta pruning; move ordering is
  derived from shallow evaluations to prune faster.

## Testing
Run the lightweight regression tests with pytest:
```bash
python -m pytest
```
