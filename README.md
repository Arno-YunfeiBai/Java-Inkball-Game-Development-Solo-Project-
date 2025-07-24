# Inkball

`Inkball` is a 2‑D puzzle arcade game written in **Java 8** with the **Processing** graphics library and managed with **Gradle**. Coloured balls ricochet around a grid of tiles – draw temporary lines to guide each one into the hole of the matching colour before the clock runs out. Capture everything and you clear the level; mis‑place a ball and your score suffers. 

## Gameplay Overview (Map shown in level.txt file)

| Symbol | Meaning |
|--------|---------|
| `X` | Grey wall: reflects balls without repainting |
| `1‑4` | Coloured walls that reflect **and** repaint the ball |
| `S` | Spawner – random entry point for queued balls |
| `Hn` | 2×2 hole of colour *n* |
| `Bn` | Ball that is present immediately at level start |
| _space_ | Empty tile |

Each level is an **18 × 18** character map; one character maps to a 32 px tile in a **576 × 640** window.

## Repository Layout

```
.
├── build.gradle
├── config.json            # Tunable gameplay parameters (no code edit needed)
├── level1.txt             # Editable level layouts
├── level2.txt
├── level3.txt
├── src/
│   ├── main/java/inkball/          # Core game logic
│   ├── main/resources/inkball/     # Sprites (ball*.png, wall*.png, …)
│   └── test/java/inkball/          # JUnit tests
└── README.md
```

`config.json` and the level text files live in the project root, while all sprite assets live under `src/main/resources/inkball/`.

## Building & Running

```bash
# Compile & launch (uses the Gradle wrapper)
./gradlew run
```

> The game window is **576 × 640 px** at **30 FPS**.

### Prerequisites

* JDK 8+ (avoid language features newer than Java 8)
* An internet connection on first build to download dependencies via Gradle.

### Testing & Coverage

```bash
./gradlew test jacocoTestReport
```

A JaCoCo HTML report is written to `build/reports/`; coverage should exceed **90 %** of branches and instructions.

## Controls

* **Left mouse drag** – draw a 10 px black line.  
* **Right click** / **Ctrl + Left** – erase the line under the cursor.  
* **Space** – pause / un‑pause (shows `*** PAUSED ***`).  
* **R** – restart level or whole game once finished.

## Configuration (no code changes required!)

All gameplay behaviour is **data‑driven**:

* **Parameters** – timers, spawn intervals, scoring, ball colours, and more live in **`config.json`**. Tweak the values, save, and just re‑run the game—no recompilation or Java edits necessary.
* **Maps** – level layouts are plain‑text files **`level1.txt`–`level3.txt`**. Edit the 18 × 18 ASCII grids (or add new `levelX.txt` files and list them in `config.json`) to design fresh stages.

```json
{
  "levels": [
    { "layout": "level1.txt", "time": 120, "spawn_interval": 10 }
  ],
  "score_increase_from_hole_capture": { "grey": 70, "orange": 50 },
  "score_decrease_from_wrong_hole":  { "grey": 0,  "orange": 25 }
}
```

## Extending the Game

Suggested extensions include bricks that break after three hits, one‑way gates, timed tiles, acceleration pads, and key‑wall mechanisms. If you add an extension, include example levels and describe the feature in your design report.

## Style & Documentation

Source code follows the **Google Java Style Guide**, is fully **Javadoc**‑commented and accompanied by a UML class diagram and ≤ 500‑word design report. Compilation and execution must succeed via **`gradle run`** on Java 8.

## License

This repository is provided for educational purposes as part of the University of Sydney **INFO1113 / COMP9003** assignment.
