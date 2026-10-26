# Tic-Tac-Toe AI

A tic-tac-toe game with a simple AI opponent, written in Python with pygame.

## What it does

- Opens a 600x600 pygame window with a 3x3 grid. The player clicks a cell to place an "O"; the AI answers with an "X".
- The AI is not minimax. Its move logic in `step_ai()`:
  1. Scans a hardcoded table of two-cell line pairs (`almost_winning_combinations`); if both cells already contain "X", it plays the third cell of that line to complete three in a row.
  2. Otherwise it picks a random empty cell.
  (Due to how the loop is written, when case 1 triggers the AI may also take an extra random move right after.)
- Win detection checks the 8 standard lines (rows, columns, diagonals) and draws a "Player Wins!" / "AI Wins!" overlay.
- On startup the script connects to a local PostgreSQL server (`127.0.0.1:5432`, user `postgres`) via psycopg2, creates a `TicTacToe` table with nine integer columns and selects from it. The database content is not used by the game logic. If the table already exists (or no server is running), the script fails at startup.

## Requirements

- Python 3
- `pygame`, `psycopg2` (`pip install pygame psycopg2-binary`)
- A running PostgreSQL instance on localhost with user `postgres`, password `1234`, and no pre-existing `TicTacToe` table in the default database (the credentials are hardcoded).

## Run

```
python TicTacToeAI.py
```
