# Vibe Coding Games

A collection of games created through **Vibe Coding**, using multiple AI models to design, generate, debug, and refine playable games.

## Results

Each game is designed to be a self-contained **HTML file**, typically containing:

* HTML structure
* CSS styling
* JavaScript game logic
* HTML5 Canvas when needed

The games can generally be opened directly in a web browser without additional setup.

## Game Types

Most games are based on familiar and well-known game genres, including:

* Puzzle games
* Endless games
* Multiplayer games
* Action and arcade games
* Strategy games
* Games with CPU opponents controlled entirely by predefined logic

The goal is to recreate or experiment with familiar mechanics while exploring how much can be accomplished through AI-assisted development.

## AI Models Used

Three AI models are primarily used, each with a different role:

* **DeepSeek**: Used to improve and clarify the user's prompt, as well as fix minor bugs and make small refinements.
* **Claude**: Used to generate the complete game from scratch based on the improved prompt, including the HTML, CSS, JavaScript, Canvas, mechanics, and UI.
* **Gemini**: Used to review Claude's generated code and fix major bugs or problems that prevent the game from working correctly.
* **Visual Studio Code AI Agent**: Used as a last resort when token limits are reached on the other three AI models, or when quick but meaningful fixes are needed. Provides efficient debugging and refinement capabilities within the VS Code environment.

This multi-AI approach makes it possible to rapidly turn game ideas into functional, self-contained browser games.
