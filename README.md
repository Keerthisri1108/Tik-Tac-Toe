# TIK-TAC-TOE
TIK TAC TOE 
Here is documentation for the Tic Tac Toe Tkinter program you provided. It covers the purpose, structure, widgets, core logic, and usage notes, plus some common issues and potential enhancements.

1) Purpose
- A simple GUI Tic Tac Toe game built with Python's Tkinter.
- Two players (X and O) take turns clicking on a 3x3 grid.
- The game detects wins (row, column, diagonal) and highlights the winning line.
- Keeps score for Player X and Player O.
- Provides Reset and New Game controls.

2) Overview of structure
- Libraries:
  - tkinter.messagebox: used to display winner dialogs.
  - tkinter: standard GUI toolkit (imported with star import in this code).
- Main window setup:
  - root: Tk instance with specified size, title, and light blue background.
  - Frames organize layout:
    - Tops: header area containing the title label.
    - MainFrame: holds LeftFrame (board) and RightFrame (score area and controls).
    - LeftFrame: Tic Tac Toe grid (buttons 1-9).
    - RightFrame: score display, reset/new game buttons, and control area split into RightFrame1 (scores) and RightFrame2 (controls).
- Variables:
  - PlayerX and PlayerO: IntVar() tracking scores for X and O.
  - click: boolean flag indicating which player's turn (True for X, False for O).
  - Buttons and UI state:
    - button1 … button9: 3x3 grid buttons.
    - Each grid button initially shows a blank space " ".
    - score-related and turn-tracking state is updated in the checker and scorekeeper functions.
- Key functions:
  - checker(button): called when a grid button is clicked. Updates the button's text to "X" or "O" depending on whose turn it is, toggles the turn, and calls scorekeeper().
  - scorekeeper(): checks all possible winning combinations for both X and O. If a win is detected, highlights winning cells, increments the corresponding player's score, and shows a messagebox informing the winner.
  - reset(): clears all grid buttons back to a blank " ", and resets button backgrounds to "gainsboro".
  - NewGame(): calls reset() and resets both players' scores to 0.

3) Widgets and layout details
- Main window
  - geometry: 1350x750
  - background: Light Blue
  - title: "tic tac toe"
- Title area
  - lblTitle: large bold label displaying "Tic Tac Toe Game"
- Board area (LeftFrame)
  - 3x3 grid of Buttons (button1 to button9)
  - Each button uses Times 26 bold font, height 3, width 8
  - Default background: gainsboro
  - Command is a lambda calling checker(buttonX)
- Right side (RightFrame)
  - RightFrame1: displays scores
    - lblPlayerX: "Player X:" label
    - txtPlayerX: Entry tied to PlayerX
    - lblPlayerO: "Player O:" label
    - txtPlayerO: Entry tied to PlayerO
  - RightFrame2: control buttons
    - btnReset: "RESET" button, triggers reset()
    - btnNewGame: "NEW GAME" button, triggers NewGame()
- Winning highlight colors
  - X wins: light green
  - O wins: yellow
  - Tie/wait state remains gainsboro

4) Game logic details
- Turn management:
  - Variable click determines the current player:
    - True: place "X"
    - False: place "O"
  - After placing, the code toggles the turn and calls scorekeeper().
- Win detection (scorekeeper):
  - Checks all possible winning lines for X:
    - Rows: (1,2,3), (4,5,6), (7,8,9)
    - Diagonals: (1,5,9), (3,5,7)
    - Columns: (1,4,7), (2,5,8), (3,6,9)
  - If a line is "X", highlights those three buttons in light green, increments PlayerX score, and shows a messagebox: "Winner X - YOU HAVE WON A GAME".
  - Checks all possible winning lines for O similarly, using Yellow as highlight and "Winner O".
  - Note: The function only checks for a win; it does not explicitly detect a draw.
- Scoring:
  - PlayerX and PlayerO are IntVar()s initialized to 0.
  - When a win is detected, the corresponding player's score is incremented by 1.
- Resetting:
  - reset() clears texts of all 9 buttons to " " and resets their background to gainsboro.
- New game:
  - NewGame() calls reset() and sets scores back to 0.

5) How to run
- Prerequisites: Python 3.x with Tkinter installed (usually included by default).
- Run the script:
  - Save as a .py file, e.g., tic_tac_toe.py
  - Run: python tic_tac_toe.py
- The GUI window should appear with the Tic Tac Toe board and score area.

6) Potential issues and fixes
- Grid button text comparison uses a single space " " as the empty value. If you modify to use an empty string "", update all checks accordingly.
- Win detection occurs immediately after a move; however, there is no explicit check for a draw (all cells filled without a winner). Consider adding a draw check:
  - If all buttons text != " " and no winner found, show a draw message.
- The code uses a mix of grid/pack geometry managers in the same window (LeftFrame uses pack; RightFrame uses grid). This generally works because they are in separate containers, but can be fragile. Best practice is to keep a single geometry management approach within each container.
- Global variable usage:
  - scorekeeper relies on global state of button1..button9. This is typical for quick scripts but can be fragile if you refactor. Consider storing buttons in a list or dict for easier iteration.
- Accessibility:
  - The color highlights are not discriminable for color-blind users (light green and yellow). Consider adding an explicit "winner" label or a bold border to indicate the winner for accessibility.
- Input validation:
  - The current code assumes the entries for Player X/O are numeric and updates via IntVar. If you want manual editing of scores, this is fine; otherwise, you could disable direct editing by using read-only state or labels.

7) Enhancements (suggested)
- Implement a reset of turn indicator after New Game.
- Add a message/dialog prompting if a user wants to reset mid-game.
- Add a mode for playing against a CPU (AI) instead of a second human.
- Add a best-of-N matches or persistent high scores.
- Improve UI aesthetics: consistent color scheme, borders, and font choices.

8) Minimal reproducible example of core logic (conceptual)
- The essential parts are:
  - checker(button): assigns "X" or "O" based on turn, toggles turn, calls scorekeeper.
  - scorekeeper(): checks all 8 winning lines for both players, updates score, highlights winning cells, shows winner dialog.
  - reset(): clears board to initial state.
If you’d like, I can extract a compact, self-contained minimal example (1–2 pages) showing the core Tic Tac Toe logic in Python with Tkinter.

Would you like me to:
- Add a draw-detection feature and a draw message?
- Refactor the code to improve structure (e.g., store buttons in a list for easier win checking)?
- Provide a clean, commented version of the code?
