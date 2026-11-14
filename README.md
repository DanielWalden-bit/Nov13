
#include <iostream>
using namespace std;

int main() {
    char board[3][3] = {
        {'1', '2', '3'},
        {'4', '5', '6'},
        {'7', '8', '9'}
    };

    char player = 'X';
    int choice;
    bool win = false;

    while (true) {
        // Display board
        cout << "\n";
        for (int i = 0; i < 3; i++) {
            cout << " " << board[i][0] << " | "
                 << board[i][1] << " | " << board[i][2] << endl;
            if (i < 2) cout << "---|---|---" << endl;
        }

        // Player chooses a spot
        cout << "\nPlayer " << player << ", choose a spot (1-9): ";
        cin >> choice;

        if (choice < 1 || choice > 9) {
            cout << "Invalid choice. Try again.\n";
            continue;
        }

        int row = (choice - 1) / 3;
        int col = (choice - 1) % 3;

        if (board[row][col] == 'X' || board[row][col] == 'O') {
            cout << "That spot is taken. Try again.\n";
            continue;
        }

        board[row][col] = player;

        // Check for winner
        for (int i = 0; i < 3; i++) {
            if (board[i][0] == player && board[i][1] == player && board[i][2] == player)
                win = true;

            if (board[0][i] == player && board[1][i] == player && board[2][i] == player)
                win = true;
        }

        if (board[0][0] == player && board[1][1] == player && board[2][2] == player)
            win = true;

        if (board[0][2] == player && board[1][1] == player && board[2][0] == player)
            win = true;

        if (win) {
            cout << "\nPlayer " << player << " wins!\n";
            break;
        }

        // Switch players
        player = (player == 'X') ? 'O' : 'X';
    }

    return 0;
}
