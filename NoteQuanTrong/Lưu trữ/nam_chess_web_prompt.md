# Updated Prompt for Developing Nam Chess Web Application

## Overview
Create a web-based game called **Nam Chess (Cờ Nam)**, a turn-based strategy board game on a 9x9 grid, blending tactical gameplay with dice-based randomness. The game supports **online multiplayer**, **offline mode** (hot-seat or vs. AI), room creation, matchmaking, ranking (ELO system), and a **login/register system** with language selection (English and Vietnamese). Build the game using a no-code/low-code platform like **Lovable** or **v0.dev**, ensuring it is playable on modern browsers (WebGL-compatible) with a **clean, bright, and simple UI** incorporating **Vietnamese cultural elements** for piece and board design. The game should be responsive for desktop and mobile devices.

---

## Game Specifications (Updated from Nam Chess GDD)

### 1. Game Core Mechanics
- **Board**: 9x9 grid (81 cells).
  - **Home Zones**: 4 rows per player (36 cells each side).
  - **Neutral Zone**: Middle row (9 cells).
  - **King’s Zone**: 3x3 central area in each home zone where the King must stay.
- **Special Cells**:
  - **Green Cells** (4 total, 2 per side): Moving to a green cell forces the piece to move back 1 cell in the same direction.
  - **Red Cell** (1, board center): Moving to the red cell allows an additional 1-cell move in any direction.
- **Pieces** (16 per player):
  - **King (X)**: Moves 1 cell (horizontal, vertical, or diagonal) within the 3x3 King’s Zone.
  - **Pawn (D)**: 
    - In **home zone**: Moves **forward only** (toward the opponent’s side, no backward movement).
    - In **opponent’s zone**: Moves forward, sideways, or diagonally (no backward movement).
    - Only moves on dice rolls of 1, 2, or 3.
  - **Advisor (Q)**: Moves horizontal/vertical exact number of cells per dice roll. Only moves on dice rolls of 4, 5, or 6.
  - **Elephant (A)**: Moves diagonally exact number of cells per dice roll.
  - **Soldier (B)**: Moves horizontal/vertical exact number of cells per dice roll.
  - **Guard (T)**: Moves horizontal/vertical/diagonal within home zone only.
  - **Cannon (P)**: Moves horizontal/vertical; captures by jumping over exactly 1 piece (friend or foe) to land on an enemy piece.
- **Initial Setup**:
  - Row 1 (back): 2 Soldiers (B), 2 Elephants (A), 2 Advisors (Q), 2 Guards (T), 1 King (X).
  - Row 2: 2 Cannons (P) in columns 2 and 8.
  - Row 3: 5 Pawns (D) in odd columns (1, 3, 5, 7, 9).
- **Dice Mechanic**:
  - Each turn, players roll a 6-sided dice **once** (1–6), determining the number of cells a piece must move.
  - Players must select a piece with a **valid move** matching the dice roll (e.g., Advisors on 4–6, Pawns on 1–3, others on any roll if valid).
  - If no valid move exists for the dice roll, the player skips their turn.
- **Capture Rules**:
  - All pieces (except Cannon) capture by landing on an opponent’s piece.
  - Cannon captures by jumping over 1 piece to land on an enemy piece.
- **Win/Loss Conditions**:
  - Win: Capture the opponent’s King or leave them with no valid moves.
  - Draw: Mutual agreement, 3-position repetition, or 50 turns without captures.

### 2. Game Modes
- **Online Multiplayer**:
  - Players can create or join rooms to play with others.
  - Matchmaking system to find random opponents.
  - ELO-based ranking system (1000–3000, Bronze to Master).
- **Offline Mode**:
  - Hot-seat mode for 2 players on the same device.
  - Optional AI opponent (basic logic: random valid moves for simplicity in no-code platforms).
- **Room System**:
  - **Create Room**: Players create a room with a unique ID or name, shareable for others to join.
  - **View Rooms**: Display a list of open rooms with details (e.g., room name, player count, status).
  - **Join Room**: Players join an existing room by selecting from the list or entering a room ID.
- **Ranking System**:
  - Track player ELO scores (start at 1000, adjust based on match outcomes).
  - Display a leaderboard with top players (name, ELO, rank tier: Bronze, Silver, Gold, Master).
- **Login/Register System**:
  - Implement user authentication with **email-based signup/login** and optional **OAuth (Google, X platform)**.
  - Store player profiles (username, ELO, match history, achievements).
  - Support **guest mode** for players who don’t want to log in (no ranking saved).
- **Language Selection**:
  - Allow players to switch between **English** and **Vietnamese** for all UI elements, including menus, HUD, and tutorial.
  - Default to browser language or English if not specified.

### 3. UI/UX Requirements
- **Visual Design**:
  - **Theme**: Clean, bright, and simple with **Vietnamese cultural elements** (e.g., lotus motifs, traditional patterns like Đông Hồ painting style for board borders, red/gold/green color palette inspired by Vietnamese art).
  - **Board**: 2D top-down 9x9 grid with light/dark cells for normal areas, green for Green Cells, red for Red Cell.
  - **Pieces**: Design pieces with Vietnamese-inspired visuals:
    - King: Crown with imperial dragon motif.
    - Pawn: Farmer hat (nón lá) icon.
    - Advisor: Scholar robe silhouette.
    - Elephant: Stylized elephant with Vietnamese art style.
    - Soldier: Traditional warrior helmet.
    - Guard: Shield with lotus emblem.
    - Cannon: Bamboo cannon design.
  - Use a **bright color scheme** (e.g., red, gold, green, white) for a vibrant, approachable look.
- **Main Menu**:
  - Buttons: Play Online, Play Offline, Create Room, View Rooms, Leaderboard, Settings, Tutorial, Login/Register, Language Selection (English/Vietnamese toggle).
  - Settings: Adjust sound volume, toggle animations, select language.
- **Game HUD**:
  - Display current player’s turn, dice roll result, and optional 30-second turn timer.
  - Chat window for online mode (simple text-based).
  - Highlight valid pieces and valid moves based on dice roll.
  - Show captured pieces and remaining pieces for both players.
- **Animations**:
  - Smooth piece movement, highlight effects for valid moves, capture animations (e.g., fade-out for captured pieces), dice roll animation.
- **Responsive Design**:
  - Optimize for desktop (1920x1080) and mobile (portrait/landscape).
  - Support touch controls for mobile (tap to select piece, tap to move).
- **Tutorial**:
  - Interactive guide explaining board setup, piece movements (including updated Pawn rules), dice mechanics, special cells, and win conditions.
  - Available in English and Vietnamese.

### 4. Technical Requirements
- **Platform**: Build using Lovable or v0.dev for WebGL-compatible output, playable in modern browsers (Chrome, Firefox, Safari).
- **Multiplayer Backend**:
  - Use a real-time database (e.g., Firebase or platform-native solution) for room management, matchmaking, ELO tracking, and player profiles.
  - Ensure low-latency turn updates for online play.
- **Performance**:
  - Target 60 FPS on desktop, 30 FPS on mobile.
  - Optimize for WebGL with minimal assets (use vector graphics or simple sprites for pieces).
- **Login System**:
  - Implement email-based signup/login with password recovery.
  - Integrate OAuth (Google, X) for single-sign-on if supported by the platform.
  - Store player data (username, ELO, match history, achievements) in a database.
  - Allow guest mode with limited features (no ranking or profile saving).
- **Language Support**:
  - Implement a language toggle (English/Vietnamese) affecting all UI, HUD, and tutorial text.
  - Store user’s language preference in their profile (if logged in) or browser session.
- **Achievements System**:
  - Track achievements (e.g., “Win 5 matches”, “Capture 10 pieces in one game”, “Win without losing a piece”).
  - Display achievements in player profile.
- **Sound**:
  - Add sound effects for dice rolls, piece moves, captures, and special cell effects (use platform-provided assets or simple audio clips).
  - Include subtle background music inspired by Vietnamese traditional instruments (e.g., đàn bầu).

### 5. Development Guidelines
- **Frontend**:
  - Use platform’s visual editor to design the board, UI, and animations.
  - Implement drag-and-drop or click/tap interactions for piece movement.
  - Create reusable UI components (e.g., buttons, board cells, piece icons).
  - Use a bright, clean color palette (red, gold, green, white) with Vietnamese cultural motifs.
- **Backend Logic**:
  - Implement dice rolling (random 1–6, single roll per turn).
  - Validate moves based on piece rules (updated Pawn rules: forward-only in home zone, multi-directional in opponent’s zone, no backward moves).
  - Handle special cell effects (Green: move back 1; Red: move extra 1).
  - Manage turn-based flow and synchronize moves in online mode.
- **No-Code Constraints**:
  - Use platform-native logic blocks for game rules (e.g., conditionals for dice rolls, move validation, Pawn restrictions).
  - Avoid complex scripting unless supported by the platform.
- **Testing**:
  - Ensure cross-browser compatibility (Chrome, Firefox, Safari).
  - Test multiplayer stability (room creation, joining, matchmaking).
  - Verify responsive design and touch controls on mobile devices.
  - Test language toggle functionality and Vietnamese text rendering.

### 6. Deliverables
- A fully functional web-based Nam Chess game with:
  - 9x9 board with special cells (Green, Red) and Vietnamese-inspired design.
  - 16 pieces per player with updated Pawn movement rules.
  - Single dice roll per turn with move validation.
  - Online multiplayer with room creation, room list, matchmaking, and ELO ranking.
  - Offline hot-seat mode (AI optional if platform supports).
  - Login/register system (email + OAuth, guest mode).
  - Language toggle (English/Vietnamese).
  - Leaderboard and achievements system.
- Responsive UI with bright, clean design, Vietnamese cultural elements, and animations.
- Interactive tutorial in both languages.
- Deployable WebGL build hosted on a platform-compatible server.

### 7. Additional Notes
- **Visual Style**: Emphasize simplicity and clarity with a bright color scheme (red, gold, green, white). Incorporate Vietnamese cultural elements like lotus flowers, Đông Hồ patterns, or imperial motifs in piece and board design.
- **Sound**: Use sound effects for dice rolls, piece moves, captures, and special cells. Add background music with Vietnamese traditional tones (e.g., đàn bầu or flute).
- **Accessibility**: Ensure text is legible (minimum 16px font size) and UI is intuitive for all ages (8+).
- **Tagline**: “Nam Chess – Strategy meets luck, playable anytime, anywhere.”

---

## Prompt for Lovable/v0.dev
"Create a web-based strategy game called Nam Chess (Cờ Nam) using your no-code/low-code tools. The game is a 9x9 turn-based board game with 16 pieces per player, a single 6-sided dice roll per turn, and special cells (4 Green, 1 Red) affecting movement. Implement the following:

1. **Game Mechanics**: Build a 9x9 grid with home zones (4 rows per side), a neutral middle row, and 3x3 King’s Zones. Include piece types (King, Pawn, Advisor, Elephant, Soldier, Guard, Cannon) with specific movement rules (updated Pawn: forward-only in home zone, forward/sideways/diagonal in opponent’s zone, no backward moves). Players roll a 6-sided dice once per turn to determine valid pieces and move distance. Implement capture rules and special cell effects (Green: move back 1; Red: move extra 1). Win by capturing the opponent’s King or blocking all their moves.

2. **Game Modes**: Support online multiplayer with room creation, a room list view, and matchmaking. Add a ranking system (ELO, 1000–3000, Bronze to Master) with a leaderboard. Include offline hot-seat mode for 2 players on one device. Optionally, add a simple AI opponent if supported.

3. **UI/UX**: Design a **clean, bright, and simple** responsive UI for desktop and mobile with a **Vietnamese cultural theme** (lotus motifs, Đông Hồ patterns, red/gold/green palette). Include a main menu (Play Online, Play Offline, Create Room, View Rooms, Leaderboard, Settings, Tutorial, Login/Register, Language Toggle: English/Vietnamese), game HUD (turn indicator, dice result, optional 30-second timer, chat for online mode), and interactive board (highlight valid pieces/moves). Use Vietnamese-inspired piece designs (e.g., King with dragon motif, Pawn with nón lá). Add animations for moves, captures, and dice rolls. Include an interactive tutorial in both languages.

4. **Multiplayer Features**: Use a real-time database (e.g., Firebase) for room management, matchmaking, ELO tracking, and player profiles. Allow players to create rooms, view/join open rooms, and find random opponents. Synchronize turns in real-time.

5. **Login System**: Implement email-based signup/login with password recovery and optional OAuth (Google, X). Store player profiles (username, ELO, match history, achievements). Support guest mode without ranking.

6. **Language Support**: Add a toggle for English and Vietnamese, affecting all UI, HUD, and tutorial text. Store language preference in profiles or browser session.

7. **Technical Requirements**: Ensure WebGL compatibility, 60 FPS on desktop, 30 FPS on mobile. Use platform tools for board rendering, UI design, and logic (single dice roll, move validation, Pawn restrictions). Add sound effects (dice, moves, captures) and Vietnamese-inspired background music (e.g., đàn bầu).

8. **Achievements**: Track achievements like ‘Win 5 matches’ or ‘Capture 10 pieces in one game’ and display them in profiles.

Deploy the game as a WebGL build, ensuring cross-browser compatibility, mobile responsiveness, and Vietnamese text rendering. Use a bright, clean design with Vietnamese cultural elements for pieces and board."