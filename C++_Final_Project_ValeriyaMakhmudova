#include <iostream>  /* libraries for cin, cout operations
#include <cstdlib>      random number functions
#include <ctime>        initializing the random number generator */

using namespace std;
// function to print our messages with color formatting
void printMessage(string message, string color = "default") {
    if (color == "red") cout << "\033[1;31m" << message << "\033[0m" << endl;
    else if (color == "green") cout << "\033[1;32m" << message << "\033[0m" << endl;
    else if (color == "yellow") cout << "\033[1;33m" << message << "\033[0m" << endl;
    else if (color == "cyan") cout << "\033[1;36m" << message << "\033[0m" << endl;
    else cout << message << endl;
}

// character structure
struct Character {
    string name;
    string role;
    int health, maxHealth;
    int attack, defense;
    int potions, level, exp, gold;
    bool hasSword;
};

// enemy structure
struct Enemy {
    string name;
    int health, attack, defense;
};

// the process of creating characther
Character createCharacter() {
    Character player;
    printMessage("Enter your character's name: ", "cyan");
    cin >> player.name;

    printMessage("\nChoose your class:", "yellow");
    printMessage("1. Warrior (Balanced stats, 'Power Strike' skill)");
    printMessage("2. Mage (High attack, 'Fireball' skill)");
    printMessage("3. Archer (High defense, 'Double Shot' skill)");

    int choice;
    cin >> choice;

    if (choice == 1) {
        player.role = "Warrior";
        player.health = player.maxHealth = 100;
        player.attack = 15;
        player.defense = 10;
    }
    else if (choice == 2) {
        player.role = "Mage";
        player.health = player.maxHealth = 80;
        player.attack = 20;
        player.defense = 5;
    }
    else {
        player.role = "Archer";
        player.health = player.maxHealth = 90;
        player.attack = 17;
        player.defense = 8;
    }

    player.potions = 5;  
    player.level = 1;
    player.exp = 0;
    player.gold = 50;
    player.hasSword = false;

    return player;
}

// display player status
void showStatus(Character& player) {
    printMessage("\n=== PLAYER STATUS ===", "cyan");
    cout << "Name: " << player.name << " (" << player.role << ")" << endl;
    cout << "HP: " << player.health << "/" << player.maxHealth << endl;
    cout << "Attack: " << player.attack << " | Defense: " << player.defense << endl;
    cout << "Potions: " << player.potions << " | Gold: " << player.gold << endl;
    cout << "Level: " << player.level << " | EXP: " << player.exp << "/50\n";
    cout << "Has Sword: " << (player.hasSword ? "Yes" : "No") << endl;
}

// battle system
void battle(Character& player, Enemy enemy) {
    printMessage("A wild " + enemy.name + " appears!", "red");

    while (player.health > 0 && enemy.health > 0) {
        printMessage("\n1. Attack  2. Use potion", "yellow");
        int choice;
        cin >> choice;

        if (choice == 1) { 
            int damage = max(0, (player.attack - enemy.defense) + (rand() % 7 - 3));
            printMessage("You attack the " + enemy.name + " for " + to_string(damage) + " damage!", "green");
            enemy.health -= damage;

            if (enemy.health <= 0) {
                printMessage("You defeated the " + enemy.name + "!", "green");
                player.exp += 20;
                player.gold += 20;

                if (enemy.name == "Goblin" && !player.hasSword) {
                    printMessage("The goblin dropped a sword! You take it.", "yellow");
                    player.hasSword = true;
                }

                if (player.exp >= 50) {
                    player.level++;
                    player.exp = 0;
                    player.maxHealth += 10;
                    player.health = player.maxHealth;
                    player.attack += 3;
                    player.defense += 2;
                    printMessage("Level up! Your status has increased!", "cyan");
                }
                return;
            }
        }
        else if (choice == 2) {
            if (player.potions > 0) {
                player.potions--;
                player.health = min(player.maxHealth, player.health + 20);
                printMessage("You used a potion!", "yellow");
            }
            else {
                printMessage("You have no potions!", "red");
            }
        }
        else {
            printMessage("Invalid choice!", "red");
            continue;
        }

        int enemyDamage = max(0, (enemy.attack - player.defense) + (rand() % 7 - 3));
        
        if (rand() % 5 == 0) {  // 20% chance of critical hit
            enemyDamage *= 2;
            printMessage(enemy.name + " lands a CRITICAL HIT!", "red");
        }

        printMessage(enemy.name + " attacks you for " + to_string(enemyDamage) + " damage!", "red");
        player.health -= enemyDamage;

        if (player.health <= 0) {
            printMessage("You have been defeated...", "red");
        }
    }
}

// 1 way: exploring the forest
void forest(Character& player) {
    printMessage("\nYou walk through the dark forest...", "cyan");

    if (rand() % 2 == 0) {  // 50% chance of encountering a goblin
        Enemy goblin = {"Goblin", 35, 12, 3}; 
        battle(player, goblin);
    }
    else {
        printMessage("The forest is quiet... Nothing happens.", "yellow");
    }
}

// way 2: the dungeon
void dungeon(Character& player) {
    if (!player.hasSword) {
        printMessage("The dungeon is too dangerous... You should prepare first!", "red");
        return;
    }

    printMessage("\nYou enter the dark dungeon...", "cyan");
    Enemy darkLord = {"Dark Lord", 120, 25, 7};  
    battle(player, darkLord);

    if (player.health > 0) {
        printMessage("You defeated the Dark Lord! The world is saved!", "green");
    }
}

// main game function
int main() {
    srand(time(0)); 
    Character player = createCharacter();

    while (player.health > 0) {  // game looping while the player is alive
        printMessage("\nWhat do you want to do?", "yellow");
        printMessage("1. Explore the forest");
        printMessage("2. Enter the dungeon");
        printMessage("3. Show status");
        printMessage("4. Exit game");
        int choice;
        cin >> choice;

        if (choice == 1) forest(player);
        else if (choice == 2) dungeon(player);
        else if (choice == 3) showStatus(player);
        else if (choice == 4) break;
        else printMessage("Invalid choice!", "red");
    }

    printMessage("Thanks for playing!", "cyan");
    return 0;
}
