#include <SFML/Graphics.hpp>
#include <iostream>
#include <fstream>
#include <string>
#include <vector>
#include <cstdlib>
#include <ctime>
#include <algorithm>
#include <cstring>
#include <limits>

using namespace std;

// ====================== GLOBAL CONSTANTS ======================
const int WINDOW_WIDTH = 800;
const int WINDOW_HEIGHT = 400;
const int GROUND_LEVEL = 300;
const int DINO_WIDTH = 50;
const int DINO_HEIGHT = 50;
const int OBSTACLE_WIDTH = 30;
const int OBSTACLE_HEIGHT = 50;

// Difficulty settings
const int EASY_SPEED = 4;
const int MEDIUM_SPEED = 7;
const int HARD_SPEED = 10;
const float EASY_SPAWN = 2.0f;
const float MEDIUM_SPAWN = 1.5f;
const float HARD_SPAWN = 1.0f;

// ====================== STRUCTS ======================
struct Obstacle {
    int x, y;
};

struct PlayerStats {
    char name[50];
    int gamesPlayed;
    int easyPlayed;
    int mediumPlayed;
    int hardPlayed;
    int totalScore;
    int bestEasy;
    int bestMedium;
    int bestHard;

    // Constructor to initialize values
    PlayerStats() {
        name[0] = '\0';
        gamesPlayed = 0;
        easyPlayed = 0;
        mediumPlayed = 0;
        hardPlayed = 0;
        totalScore = 0;
        bestEasy = 0;
        bestMedium = 0;
        bestHard = 0;
    }
};

struct GameState {
    int playerX, playerY;
    float jumpVelocity;
    bool isJumping;
    vector<Obstacle> obstacles;
    int score;
    int obstacleSpeed;
    float spawnInterval;
    bool isRunning;
};

// ====================== FUNCTION PROTOTYPES ======================
// ------------------- GROUP A: PLAYER, MENU, FILES -------------------
void showMainMenu();
int getMenuChoice();
void handleMenuChoice(int choice);
void showHelp();
void getPlayerName(char playerName[]);
int chooseDifficulty();
void showHighScoresMenu();
void showHighScores(int difficulty);
void showPlayerScores();
bool fileExists(const char* filename);
void saveHighScore(int difficulty, const char name[], int score);
void savePlayerStats(const char name[], int difficulty, int score);
void loadAllPlayers(PlayerStats*& arr, int& count);
void saveAllPlayers(PlayerStats* arr, int count);
int findPlayerIndex(PlayerStats* arr, int count, const char name[]);
void updatePlayerRecord(PlayerStats& p, int difficulty, int score);
void expandPlayerArray(PlayerStats*& arr, int& count);
void showPlayerStats(const PlayerStats& p);
void clearScreen();
void pauseScreen();
void clearInputBuffer();
bool isValidName(const char* name);

// ------------------- GROUP B: GAMEPLAY LOGIC -------------------
void startNewGame();
void startGame(int difficulty, const char playerName[]);
void initializeGame(GameState& game, int difficulty);
void updateDino(GameState& game);
void updateObstacles(GameState& game);
bool checkCollision(const GameState& game);
void updateScore(GameState& game);
void gameOverScreen(int score, const char playerName[], int difficulty);
void setDifficultyParams(GameState& game, int difficulty);
void spawnObstacle(GameState& game);

// ------------------- GROUP C: GRAPHICS + SFML -------------------
void renderGame(sf::RenderWindow& window, const GameState& game);
void drawGround(sf::RenderWindow& window);
void drawDino(sf::RenderWindow& window, const GameState& game);
void drawObstacles(sf::RenderWindow& window, const GameState& game);
void drawScore(sf::RenderWindow& window, int score);
void gameLoop(int difficulty, const char playerName[]);

// Simple text-based game simulation for testing
void textBasedGameLoop(int difficulty, const char playerName[]);

// ====================== MAIN FUNCTION ======================
int main() {
    srand(static_cast<unsigned int>(time(0)));

    while (true) {
        showMainMenu();
        int choice = getMenuChoice();
        if (choice == 5) {
            cout << "\nThank you for playing! Goodbye!\n";
            break;
        }
        handleMenuChoice(choice);
    }

    return 0;
}

// ====================== GROUP A: PLAYER, MENU, FILES ======================
void clearScreen() {

}

void pauseScreen() {
   
}

void clearInputBuffer() {
 
}

bool isValidName(const char* name) {
   
}

void showMainMenu() {
   
}

int getMenuChoice() {
    
}

void handleMenuChoice(int choice) {
    
}

void showHelp() {

}

void getPlayerName(char playerName[]) {
   
}

int chooseDifficulty() {
    
}

void showHighScoresMenu() {
   
}

void showHighScores(int difficulty) {
   
}

void showPlayerScores() {
    
}

bool fileExists(const char* filename) {
  
}

void saveHighScore(int difficulty, const char name[], int score) {
    
}

void savePlayerStats(const char name[], int difficulty, int score) {
   
}

void loadAllPlayers(PlayerStats*& arr, int& count) {
}
void saveAllPlayers(PlayerStats* arr, int count) {
   

int findPlayerIndex(PlayerStats* arr, int count, const char name[]) {
   
}

void updatePlayerRecord(PlayerStats& p, int difficulty, int score) {
   
}

void expandPlayerArray(PlayerStats*& arr, int& count) {
}

void showPlayerStats(const PlayerStats& p) {
  
}

// ====================== GROUP B: GAMEPLAY LOGIC ======================
void startNewGame() {
    char playerName[50];
    getPlayerName(playerName);
    int diff = chooseDifficulty();
    startGame(diff, playerName);
}

void startGame(int difficulty, const char playerName[]) {
    gameLoop(difficulty, playerName);  // Use SFML game loop
}

void initializeGame(GameState& game, int difficulty) {
    game.playerX = 50;
    game.playerY = GROUND_LEVEL;
    game.isJumping = false;
    game.jumpVelocity = 0;
    game.score = 0;
    game.obstacles.clear();
    game.isRunning = true;

    setDifficultyParams(game, difficulty);
}

void setDifficultyParams(GameState& game, int difficulty) {
    switch (difficulty) {
    case 1: // Easy
        game.obstacleSpeed = EASY_SPEED;
        game.spawnInterval = EASY_SPAWN;
        break;
    case 2: // Medium
        game.obstacleSpeed = MEDIUM_SPEED;
        game.spawnInterval = MEDIUM_SPAWN;
        break;
    case 3: // Hard
        game.obstacleSpeed = HARD_SPEED;
        game.spawnInterval = HARD_SPAWN;
        break;
    default:
        game.obstacleSpeed = MEDIUM_SPEED;
        game.spawnInterval = MEDIUM_SPAWN;
    }
}

void updateDino(GameState& game) {
    if (game.isJumping) {
        game.playerY += static_cast<int>(game.jumpVelocity);
        game.jumpVelocity += 0.8f;

        if (game.playerY >= GROUND_LEVEL) {
            game.playerY = GROUND_LEVEL;
            game.isJumping = false;
            game.jumpVelocity = 0;
        }
    }
}

void updateObstacles(GameState& game) {
    for (size_t i = 0; i < game.obstacles.size(); i++) {
        game.obstacles[i].x -= game.obstacleSpeed;
    }

    // Remove off-screen obstacles
    game.obstacles.erase(
        remove_if(game.obstacles.begin(), game.obstacles.end(),
            [](const Obstacle& o) { return o.x < -OBSTACLE_WIDTH; }),
        game.obstacles.end()
    );
}

bool checkCollision(const GameState& game) {
    for (const auto& o : game.obstacles) {
        // Simple rectangle collision
        if (game.playerX + DINO_WIDTH > o.x &&
            game.playerX < o.x + OBSTACLE_WIDTH &&
            game.playerY + DINO_HEIGHT > o.y) {
            return true;
        }
    }
    return false;
}

void updateScore(GameState& game) {
    game.score++;
}

void spawnObstacle(GameState& game) {
    Obstacle obs;
    obs.x = WINDOW_WIDTH;
    obs.y = GROUND_LEVEL;
    game.obstacles.push_back(obs);
}

void gameOverScreen(int score, const char playerName[], int difficulty) {
    clearScreen();
    cout << "\n========================================\n";
    cout << "             GAME OVER!                \n";
    cout << "========================================\n";
    cout << "Player: " << playerName << "\n";
    cout << "Final Score: " << score << "\n";

    string diffName;
    switch (difficulty) {
    case 1: diffName = "Easy"; break;
    case 2: diffName = "Medium"; break;
    case 3: diffName = "Hard"; break;
    }
    cout << "Difficulty: " << diffName << "\n";
    cout << "========================================\n";

    saveHighScore(difficulty, playerName, score);
    savePlayerStats(playerName, difficulty, score);

    cout << "Score saved successfully!\n";
    pauseScreen();
}

// ====================== GROUP C: GRAPHICS + SFML ======================

void renderGame(sf::RenderWindow& window, const GameState& game) {
    

void drawGround(sf::RenderWindow& window) {
    
}

void drawDino(sf::RenderWindow& window, const GameState& game) {
   
}

void drawObstacles(sf::RenderWindow& window, const GameState& game) {
   
    }
}

void drawScore(sf::RenderWindow& window, int score) {
    // Note: Font rendering requires a font file
    // For now, score is displayed in console
}

void gameLoop(int difficulty, const char playerName[]) {
    GameState game;
    initializeGame(game, difficulty);

    // SFML 3.x: Create window with sf::VideoMode using brace initialization
    sf::RenderWindow window(sf::VideoMode(sf::Vector2u(static_cast<unsigned int>(WINDOW_WIDTH),
        static_cast<unsigned int>(WINDOW_HEIGHT))),
        "Chrome Dino Game");
    window.setFramerateLimit(60);

    sf::Clock clock;
    float spawnTimer = 0;

        
            

        float dt = clock.restart().asSeconds();
        spawnTimer += dt;

        // Update game state
        updateDino(game);
        updateObstacles(game);

        // Spawn obstacles
        if (spawnTimer > game.spawnInterval) {
           
        }

        // Check collision
        if (checkCollision(game)) {
            
        }

        updateScore(game);

       
    }
}

// ====================== TEXT-BASED GAME SIMULATION FOR TESTING ======================
void textBasedGameLoop(int difficulty, const char playerName[]) {
    GameState game;
    initializeGame(game, difficulty);

    cout << "\n========================================\n";
    cout << "        GAME STARTED (TEXT MODE)       \n";
    cout << "========================================\n";
    cout << "Player: " << playerName << "\n";

    string diffName;
    switch (difficulty) {
    case 1: diffName = "Easy"; break;
    case 2: diffName = "Medium"; break;
    case 3: diffName = "Hard"; break;
    }
    cout << "Difficulty: " << diffName << "\n";
    cout << "Speed: " << game.obstacleSpeed << "\n";
    cout << "Spawn Interval: " << game.spawnInterval << "s\n";
    cout << "========================================\n";
    cout << "\nSimulating game...\n";

    // Simulate game for testing
    float gameTime = 0;
    float spawnTimer = 0;
    const float timeStep = 0.1f;
    const float maxGameTime = 10.0f;  // Simulate 10 seconds

    while (gameTime < maxGameTime && game.isRunning) {
        gameTime += timeStep;
        spawnTimer += timeStep;

        // Simulate jump every 2 seconds
        if (static_cast<int>(gameTime) % 2 == 0 && !game.isJumping && gameTime > 0.5f) {
            game.isJumping = true;
            game.jumpVelocity = -15.0f;
            cout << "[" << static_cast<int>(gameTime) << "s] JUMP!\n";
        }

        // Update game
        updateDino(game);
        updateObstacles(game);

        // Spawn obstacles
        if (spawnTimer > game.spawnInterval) {
            spawnObstacle(game);
            spawnTimer = 0;
            cout << "[" << static_cast<int>(gameTime) << "s] Obstacle spawned!\n";
        }

        // Check collision
        if (checkCollision(game)) {
            cout << "\n[" << static_cast<int>(gameTime) << "s] COLLISION DETECTED!\n";
            game.isRunning = false;
            break;
        }

        updateScore(game);

        // Show status every 2 seconds
        if (static_cast<int>(gameTime * 10) % 20 == 0) {
            cout << "[" << static_cast<int>(gameTime) << "s] Score: " << game.score
                << " | Obstacles: " << game.obstacles.size()
                << " | Dino Y: " << game.playerY << "\n";
        }
    }

    if (gameTime >= maxGameTime) {
        cout << "\nSimulation completed successfully!\n";
    }

    cout << "\n========================================\n";
    cout << "         SIMULATION ENDED              \n";
    cout << "========================================\n";
    cout << "Time Survived: " << static_cast<int>(gameTime) << " seconds\n";
    cout << "Final Score: " << game.score << "\n";
    cout << "Obstacles Dodged: " << game.obstacles.size() << "\n";
    cout << "========================================\n";

    gameOverScreen(game.score, playerName, difficulty);
}
