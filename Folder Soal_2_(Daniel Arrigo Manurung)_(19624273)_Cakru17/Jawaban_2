#include <iostream>
#include <cmath>
#include <cstdlib>
#include <ctime>

class Robot {
public:
    int healthpoints;
    int attack;
    int speed;

    Robot(int hp, int atk, int spd) : healthpoints(hp), attack(atk), speed(spd) {}
};

class OptimusPrime : public Robot {
public:
    OptimusPrime() : Robot(150, 75, 25) {}
};

class Bumblebee : public Robot {
public:
    Bumblebee() : Robot(100, 100, 50) {}
};

class Megatron : public Robot {
public:
    Megatron() : Robot(55, 165, 30) {}
};

class Starscream : public Robot {
public:
    Starscream() : Robot(85, 105, 60) {}
};

class Moves {
public:
    int damage;
    int accuracy;
    Moves(int dmg, int acc) : damage(dmg), accuracy(acc) {}
};

class Uppercut : public Moves {
public:
    Uppercut() : Moves(60, 85) {}
};

class TakeDown : public Moves {
public:
    TakeDown() : Moves(85, 35) {}
};

class LowKick : public Moves {
public:
    LowKick() : Moves(45, 100) {}
};

class Headbutt : public Moves {
public:
    Headbutt() : Moves(75, 50) {}
};

class Game {
public:
    Robot* selectedRobots[2] = {nullptr, nullptr};
    Uppercut uppercut;
    TakeDown takeDown;
    LowKick lowKick;
    Headbutt headbutt;

    void add_robot() {
        const char* robots[4] = {"Optimus Prime", "Bumblebee", "Megatron", "Starscream"};

        for (int counter = 0; counter < 2; counter++) {
            std::cout << "Choose Robots For Battle\n";
            std::cout << "(1) Optimus Prime\n";
            std::cout << "(2) Bumblebee\n";
            std::cout << "(3) Megatron\n";
            std::cout << "(4) Starscream\n";

            int choice;
            std::cin >> choice;

            switch (choice) {
                case 1: selectedRobots[counter] = new OptimusPrime(); break;
                case 2: selectedRobots[counter] = new Bumblebee(); break;
                case 3: selectedRobots[counter] = new Megatron(); break;
                case 4: selectedRobots[counter] = new Starscream(); break;
                default: std::cout << "Invalid choice\n"; return;
            }

            std::cout << "You Chose " << robots[choice - 1] << "\n";
            if (counter == 0) {
                std::cout << "Choose your next robot\n";
            }
        }

        std::cout << "Battle Start!\n";
        start_game();
    }

    void start_game() {
        std::cout << "Battle between selected robots begins!\n";
        int firstRobot = selectedRobots[0]->speed > selectedRobots[1]->speed ? 0 : 1;

        while (selectedRobots[0]->healthpoints > 0 && selectedRobots[1]->healthpoints > 0) {
            take_turn(firstRobot);
            firstRobot = 1 - firstRobot;  // Alternate turns
        }

        if (selectedRobots[0]->healthpoints <= 0) {
            std::cout << "Robot 2 Wins!\n";
        } else {
            std::cout << "Robot 1 Wins!\n";
        }
    }

    void take_turn(int robotIndex) {
        std::cout << "Robot " << robotIndex + 1 << "'s turn! Pick A Move:\n";
        std::cout << "1. Uppercut (60 Power, 85 Accuracy)\n";
        std::cout << "2. TakeDown (100 Power, 35 Accuracy)\n";
        std::cout << "3. LowKick (45 Power, 100 Accuracy)\n";
        std::cout << "4. HeadButt (75 Power, 50 Accuracy)\n";

        int choice;
        std::cin >> choice;

        Moves* selectedMove;
        switch (choice) {
            case 1: selectedMove = &uppercut; break;
            case 2: selectedMove = &takeDown; break;
            case 3: selectedMove = &lowKick; break;
            case 4: selectedMove = &headbutt; break;
            default: std::cout << "Invalid choice\n"; return;
        }

       if (attack_hits(selectedMove->accuracy)) {
    int opponent = 1 - robotIndex;
    
    int totalDamage = selectedMove->damage + selectedRobots[robotIndex]->attack/5;
    selectedRobots[opponent]->healthpoints -= totalDamage;  
    std::cout << "Hit! Robot " << opponent + 1 << " takes " << totalDamage << " damage!\n";  
    std::cout << "Robot " << opponent + 1 << " now has " << selectedRobots[opponent]->healthpoints << " HP left.\n";
} else {
    std::cout << "Missed!\n";
}
    }

    bool attack_hits(int accuracy) {
        return rand() % 100 < accuracy;
    }

    ~Game() {
        delete selectedRobots[0];
        delete selectedRobots[1];
    }
};

int main() {
    srand(static_cast<unsigned>(time(0)));  
    std::cout << "Welcome to Battle Of Robots\n";
    Game game;
    game.add_robot();
    return 0;
}
