# CPSC_FINAL_Project
1 · What’s in this repo?

roulette_duel.py      ← the entire game: rules, AI, and CLI
That one script contains all logic and user interaction. No extra packages are required—just Python 3.8+.

2 · How the code is organised inside roulette_duel.py
Line range    Section	Key classes / functions	What it does
1 – 110	      Config + Gun	USE_MC, MC_SAMPLES, class Gun	Toggles Monte-Carlo search; handgun model with fire(), eject(), clone(), and reload().
120 – 210	    Player + Items	class Player, use_item()	Base player, life tracking, item effects (cigarettes, crystal, sand, whiskey).
215 – 305	    Human interface	class HumanPlayer	Simple input / print prompts; crystal grants an extra decision loop.
310 – 460	    AI opponents	class AIPlayer	- mc_decide() → depth-1 Monte-Carlo expectiminimax
                                            - execute() → carries out the chosen move
                                            - simple_heuristic() fallback if USE_MC = False.
465 – 565	    Game loop	class Game	Coin-flip for first move, turn handling, auto-reload, win detection.
569 – end	    Entrypoint	if __name__ == \"__main__\":	Seeds RNG and starts Game().play().

3 Running the game
python roulette_duel.py
Call heads/tails in the prompt.

Each round you must fire (f) or type an item name.

The AI responds instantly.

First to hit zero lives loses.

4 Key algorithms
Monte-Carlo sampling – 20 random cylinder permutations per turn (Gun.clone()).

Depth-1 expectiminimax – evaluates
AI action → chance (bullet/blank) → human fires
inside each sample (AIPlayer.mc_decide).

Utility = AI lives − Human lives; picks max average.

Set USE_MC = False near the top if you want the original static-rule AI.

5 Modifying / Extending
Change item behaviour – edit Player.use_item().

Add a GUI – import Game, call game.play_turn(action) from buttons.

Increase AI foresight – raise MC_SAMPLES or add a second ply inside mc_decide().

6 Requirements
Python 3.8 or newer

No external libraries needed (standard random, dataclasses only).

Optional: install pygame if you prototype a graphical front-end.
