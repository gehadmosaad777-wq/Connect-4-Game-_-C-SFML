#include <iostream>
#include <ctime>
#include <string>

using namespace std;

   int main() {
    cout << "\t\t**************************************************************" << endl;
    cout << "\t\t**************************************************************" << endl << endl;
    cout << "\t\t XXXXX   XXXXX   X   X   X   X   XXXXX   XXXXX   XXXXX    XX  " << endl;
    cout << "\t\t X       X   X   XX  X   XX  X   X       X         X     X X  " << endl;
    cout << "\t\t X       X   X   X X X   X X X   XXXX    X         X    XXXXX " << endl;
    cout << "\t\t X       X   X   X  XX   X  XX   X       X         X       X  " << endl;
    cout << "\t\t XXXXX   XXXXX   X   X   X   X   XXXXX   XXXXX     X       X  G   A   M   E  " << endl << endl;
    cout << "\t\t**************************************************************" << endl;
    cout << "\t\t**************************************************************" << endl;

    cout << "\n\t\t\t   >>> Get ready for an exciting challenge! <<<\n";
    cout << "\t\t\t   ========================================\n";

    cout << "\t\t          __________________________________________\n";
    cout << "\t\t         |                                          |\n";
    cout << "\t\t         |          --- QUICK GAME RULES ---        |\n";
    cout << "\t\t         |                                          |\n";
    cout << "\t\t         |  [1] Connect 4 symbols in a row to win.  |\n";
    cout << "\t\t         |  [2] Horizontal, Vertical, or Diagonal.  |\n";
    cout << "\t\t         |  [3] Don't let the opponent block you!   |\n";
    cout << "\t\t         |__________________________________________|\n\n";
    cout << "* Note: Players take turns dropping a disc into a column, and the first to connect four wins." << endl;
    cout << endl;

    string s;
    cout << "Press any key start the game..." << endl;
    cin >> s;

    //Game preparatin massege.
    // ask you to press any key to start game

    int mode;
    cout << "Please ,Choose Game Mode: \n";
    cout << "Click 1 For Player Vs Player \n";
    cout << "Click 2 For Player Vs Computer\n";
    cin >> mode;

    // We explain to player by sending messages to choose the game mode.
    //If the player choose mode 1, it will be player Vs. player , and if the player choose mode 2, it will be player Vs. computer.

    string name1, name2;
    char cho1, cho2;
    cout << "Player 1, Enter your name:" << endl;
    cin >> name1;
    cout << "Enter your character :" << endl;
    cin >> cho1;

    // We ask the player to enter his name and the letter he will play with ( X or O or anything else ).

    if (mode == 1) {
        cout << "Player 2 , Enter your name:" << endl;
        cin >> name2;
        cout << "Enter your character :" << endl;
        cin >> cho2;

        // We use IF if the player chooses option 1 and plays player Vs. player.
        // Then the second player starts by entering his name and the letter he will play with during the game.

        while (cho2 == cho1) {
            cout << "Character already taken by Player 1. Please choose a different character: " << endl;
            cin >> cho2;
        }

        // We use while to prevent the second player from choosing the same letter as the first player.
        // The loop repeats until the other player chooses a different letter.

    } else {
        name2 = "Computer";
        if (cho1 == 'O' || cho1 == 'o')
            cho2 = 'X';
        else
            cho2 = 'O';
    }

    // The computer is named constant "Computer" and its letter is O.

        int score1 = 0;
      // to count wins for Player 1
    int score2 = 0;
    // to count wins for Player 2 or Computer
    char playAgain;
    // to play again

    // We add two variables to record the number of times each player won.
    // We put them outside the loop so their value doesn't change when we play again.

    do {
        srand(time(NULL));

        // We enable randomness so the computer selects random columns each time.

        char grid[6][7];

        // We begin by creating a 6 rows & 7 columns board.

        for (int i = 0; i < 6; i++) {
            for (int j = 0; j < 7; j++) {
                grid[i][j] = ' ';
            }
        }

        // We use nested loops and clear the board.
        //The first loop is for the rows and the second loop is for the columns.
        //Then we use arrays to make all cells empty initially.

        int player = 1;
        bool gameOver = false;
        int moves = 0;

        // We start by entering the game control variables:
        //who will play (1 or 2 players), gameover (to end the game), moves (for a tie and count the number of moves).

        while (gameOver == false) {
            cout << "\n";

            //The main loop of the game that keeps the game running continuously until a winner is found.

            for (int j = 1; j <= 7; j++) {
                cout << "  " << j << " ";
            }
            cout << "\n";

            for (int j = 0; j < 7; j++) {
                cout << "+---";
            }
            cout << "+\n";

            // We use a for loop to draw the grid.
            // The first loop is to number the columns and the second loop is to draw the borders.

            for (int i = 0; i < 6; i++) {
                for (int j = 0; j < 7; j++) {
                    cout << "| " << grid[i][j] << " ";
                }
                cout << "|\n";
                for (int j = 0; j < 7; j++) {
                    cout << "+---";
                }
                cout << "+\n";
            }
            cout << "\n";

            // We use nested loops to draw content within boundaries;
            // the outer loops are for rows and the inner loops are for columns.

            char input;
            int col;

            // We begin by recording the movements.

            if (player == 1) {
                    do {
                    cout << "Player " << name1 << " (" << cho1 << "), choose column (1-7): ";
                cin >> input;
                if (input >= '1' && input <= '7') {
               col = input - '0';
            } else {
              cout << "Invalid move! Try again.\n";
               }

                    }
          while (input < '1' || input > '7');


                //cin >> col;
            } else {
                if (mode == 1) {
                        do {
                             cout << "Player " << name2 << " (" << cho2 << "), choose column (1-7): ";
                          cin >> input;

                       if (input >= '1' && input <= '7') {
                           col = input - '0';
                        } else {
                             cout << "Invalid move! Try again.\n";
                               }
              }
              while (input < '1' || input > '7');

                }
                // We use if statments to define that :
                // If it's player 1 against player 2 or against the computer.
                // Then we tell the players or the computer to choose a column.

                else {
                    // --- Advanced AI logic (Win & Block) ---
                    int bestCol = -1;
                    // Step 1: Check if Computer can win
                    for (int c = 0; c < 7; c++) {
                        if (grid[0][c] == ' ') {
                            int r = 5; while (r >= 0 && grid[r][c] != ' ') r--;
                            grid[r][c] = cho2;
                            bool win = false;
                            for (int i=0; i<6; i++)
                                for (int j=0; j<4; j++)
                                if (grid[i][j]==cho2 &&
                                    grid[i][j+1]==cho2 &&
                                    grid[i][j+2]==cho2 &&
                                     grid[i][j+3]==cho2)
                                     win=true;
                            for (int i=0; i<3; i++)
                            for (int j=0; j<7; j++)
                            if (grid[i][j]==cho2 &&
                                 grid[i+1][j]==cho2 &&
                                 grid[i+2][j]==cho2 &&
                                 grid[i+3][j]==cho2)
                                 win=true;
                            for (int i=0; i<3; i++)
                            for (int j=0; j<4; j++)
                            if (grid[i][j]==cho2 &&
                                grid[i+1][j+1]==cho2 &&
                                grid[i+2][j+2]==cho2 &&
                                grid[i+3][j+3]==cho2)
                                win=true;
                            for (int i=3; i<6; i++)
                            for (int j=0; j<4; j++)
                            if (grid[i][j]==cho2 &&
                                grid[i-1][j+1]==cho2 &&
                                grid[i-2][j+2]==cho2 &&
                                grid[i-3][j+3]==cho2)
                                win=true;
                            grid[r][c] = ' ';
                            if (win) {
                                    bestCol = c + 1;
                            break;
                             }
                        }
                    }
                    // Step 2: Block player if no win found
                    if (bestCol == -1) {
                        for (int c = 0; c < 7; c++) {
                            if (grid[0][c] == ' ') {
                                int r = 5;
                                while (r >= 0 && grid[r][c] != ' ')
                                    r--;
                                grid[r][c] = cho1;
                                bool block = false;
                                for (int i=0; i<6; i++){
                                    for (int j=0; j<4; j++){
                                      if (grid[i][j]==cho1 &&
                                          grid[i][j+1]==cho1 &&
                                          grid[i][j+2]==cho1 &&
                                          grid[i][j+3]==cho1)
                                    block=true;
                                }
                         }
                                for (int i=0; i<3; i++){
                                    for (int j=0; j<7; j++){
                                      if (grid[i][j]==cho1 &&
                                          grid[i+1][j]==cho1 &&
                                          grid[i+2][j]==cho1 &&
                                          grid[i+3][j]==cho1)
                                    block=true;
                                     }
                                }
                                for (int i=0; i<3; i++){
                                    for (int j=0; j<4; j++){
                                      if (grid[i][j]==cho1 &&
                                          grid[i+1][j+1]==cho1 &&
                                          grid[i+2][j+2]==cho1 &&
                                          grid[i+3][j+3]==cho1)
                                     block=true;
                                     }
                                }
                                for (int i=3; i<6; i++){
                                    for (int j=0; j<4; j++){
                                      if (grid[i][j]==cho1 &&
                                          grid[i-1][j+1]==cho1 &&
                                          grid[i-2][j+2]==cho1 &&
                                          grid[i-3][j+3]==cho1)
                                    block=true;
                                    }
                                }
                                grid[r][c] = ' ';
                                if (block) { bestCol = c + 1;
                                break;
                                }
                            }
                        }
                    }
                    if (bestCol == -1)
                        do {
                             bestCol = rand () % 7 + 1;
                    }
                    while (grid[0][bestCol - 1] != ' ');
                    col = bestCol;
                    cout << "Computer chooses column: " << col << endl;
                }
            }
            col--;

            if (col >= 0 && col < 7 && grid[0][col] == ' ')
            // We use an if statement to check if a column is valid or not full.
            {
                for (int i = 5; i >= 0; i--) {
                    if (grid[i][col] == ' ') {
                        if (player == 1) {
                            grid[i][col] = cho1;
                        } else {
                            grid[i][col] = cho2;
                        }
                        moves++;
                        break;
                    }
                }

                // We use a loop to drop the piece downwards (i.e., a loop from bottom to top), meaning the first empty slot where the piece is placed.

                char character = (player == 1) ? cho1 : cho2;

                for (int r = 0; r < 6; r++) {
                    for (int c = 0; c < 4; c++) {
                        if (grid[r][c] == character &&
                            grid[r][c + 1] == character &&
                            grid[r][c + 2] == character &&
                            grid[r][c + 3] == character)
                            {
                            gameOver = true;
                        }
                    }
                }

                //We begin by verifying the win.
                // first horizontally,by make rows constant and add the columns.

                for (int r = 0; r < 3; r++) {
                    for (int c = 0; c < 7; c++) {
                        if (grid[r][c] == character &&
                            grid[r + 1][c] == character &&
                            grid[r + 2][c] == character &&
                            grid[r + 3][c] == character)
                            {
                            gameOver = true;
                        }
                    }
                }

                // We verify verticality by costant the columns and increasing the rows.

                for (int r = 0; r < 3; r++) {
                    for (int c = 0; c < 4; c++) {
                        if (grid[r][c] == character &&
                            grid[r + 1][c + 1] == character &&
                            grid[r + 2][c + 2] == character &&
                            grid[r + 3][c + 3] == character)
                            {
                            gameOver = true;
                        }
                    }
                }
                //We verify the win using the rightward slant and increase the rows & columns.

                for (int r = 3; r < 6; r++) {
                    for (int c = 0; c < 4; c++) {
                        if (grid[r][c] == character &&
                            grid[r - 1][c + 1] == character &&
                            grid[r - 2][c + 2] == character &&
                            grid[r - 3][c + 3] == character) {
                            gameOver = true;
                        }
                    }
                }

                // Finally, we check the leftward slant by increasing the number of columns and decreasing the number of rows.

                if (gameOver == true) {
                    // We check if it's a win or a draw.
                    // We use `if statement` to win if `gameover = true`

                    cout << "\n";
                    for (int j = 1; j <= 7; j++) {
                            cout << "  " << j << " ";
                    }
                    cout << "\n";
                    for (int j = 0; j < 7; j++) {
                            cout << "+---";
                    }
                    cout << "+\n";
                    for (int i = 0; i < 6; i++) {
                        for (int j = 0; j < 7; j++) {
                                cout << "| " << grid[i][j] << " ";
                        }
                        cout << "|\n";
                        for (int j = 0; j < 7; j++) {
                                cout << "+---";
                                }
                              cout << "+\n";
                    }

                    string winnerName = (player == 1) ? name1 : name2;
                    cout << "\nGame Over! Player " << winnerName << " Wins!\n";

                    if (player == 1) score1++;
                    else score2++;

                    // We use the same steps at else if but to draw!
                    // Show final score results.
                    cout << "\n--- CURRENT SCORE ---\n";
                    cout << name1 << ": " << score1 << " Wins\n";
                    cout << name2 << ": " << score2 << " Wins\n";
                    cout << "---------------------\n";

                } else if (moves == 42)
                    //We use `else if` if there is a draw, meaning the total number of moves (6 rows x 7 columns = 42 move ) is 42.
                {
                    cout << "\n";
                    for (int j = 1; j <= 7; j++) {
                            cout << "  " << j << " ";
                            }
                            cout << "\n";
                    for (int j = 0; j < 7; j++) {
                        cout << "+---"; }
                        cout << "+\n";
                    for (int i = 0; i < 6; i++) {
                        for (int j = 0; j < 7; j++) {
                            cout << "| " << grid[i][j] << " ";
                            }
                            cout << "|\n";
                        for (int j = 0; j < 7; j++) {
                            cout << "+---";
                            }
                        cout << "+\n";
                    }

                    cout << "\nGame Over ! It's a Draw!\n";
                    gameOver = true;

                    // Show score even in draw.
                    cout << "\n--- CURRENT SCORE ---\n";
                    cout << name1 << ": " << score1 << " Wins\n";
                    cout << name2 << ": " << score2 << " Wins\n";
                    cout << "---------------------\n";

                } else {
                    // We use "else" to substitute players if there is no win or a draw.
                    if (player == 1)
                        player = 2;
                    else
                    player = 1;
                }

            } else {
                // We use "else" (before the last one) to signal that the move is wrong if the player chooses a missing column or a full column.
                cout << "Invalid move ! Try again.\n";
            }
        }
        cout << "\nDo you want to play again with same settings? (y/n): ";
        cin >> playAgain;
        }while (playAgain == 'y' || playAgain == 'Y');

    //Thank you.

    return 0;
}
