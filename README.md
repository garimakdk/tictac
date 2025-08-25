//tictac
#include <iostream>
using namespace std;

class TicTacToe {
private:
    char board[3][3];
    char currentPlayer;

public:
    TicTacToe() {
        currentPlayer = 'X';
        char start = '1';
        for (int i = 0; i < 3; ++i)
            for (int j = 0; j < 3; ++j)
                board[i][j] = start++;
    }

    void displayBoard() {
        cout << "\n";
        for (int i = 0; i < 3; ++i) {
            cout << " ";
            for (int j = 0; j < 3; ++j) {
                cout << board[i][j];
                if (j < 2) cout << " | ";
            }
            cout << "\n";
            if (i < 2) cout << "---|---|---\n";
        }
        cout << "\n";
    }

    void switchPlayer() {
        currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
    }

    bool isValidMove(int position) {
        if (position < 1 || position > 9)
            return false;
        int row = (position - 1) / 3;
        int col = (position - 1) % 3;
        return board[row][col] != 'X' && board[row][col] != 'O';
    }

    bool makeMove(int position) {
        if (!isValidMove(position))
            return false;
        int row = (position - 1) / 3;
        int col = (position - 1) % 3;
        board[row][col] = currentPlayer;
        return true;
    }

    bool checkWin() {
        for (int i = 0; i < 3; ++i)
            if (board[i][0] == currentPlayer &&
                board[i][1] == currentPlayer &&
                board[i][2] == currentPlayer)
                return true;

        for (int i = 0; i < 3; ++i)
            if (board[0][i] == currentPlayer &&
                board[1][i] == currentPlayer &&
                board[2][i] == currentPlayer)
                return true;

        if (board[0][0] == currentPlayer &&
            board[1][1] == currentPlayer &&
            board[2][2] == currentPlayer)
            return true;

        if (board[0][2] == currentPlayer &&
            board[1][1] == currentPlayer &&
            board[2][0] == currentPlayer)
            return true;

        return false;
    }

    bool isDraw() {
        for (int i = 0; i < 3; ++i)
            for (int j = 0; j < 3; ++j)
                if (board[i][j] != 'X' && board[i][j] != 'O')
                    return false;
        return true;
        void play() {
        int move;
        bool gameOver = false;

        while (!gameOver) {
            displayBoard();
            cout << "Player " << currentPlayer << ", enter your move (1-9): ";

            cin >> move;

            // Simple input validation
            while (cin.fail() || !isValidMove(move)) {
                cin.clear();
                cin.ignore(1000, '\n');
                cout << "Invalid move! Try again (1-9): ";
                cin >> move;
            }

            makeMove(move);

            if (checkWin()) {
                displayBoard();
                cout << "Player " << currentPlayer << " wins!\n";
                gameOver = true;
            } else if (isDraw()) {
                displayBoard();
                cout << "It's a draw!\n";
                gameOver = true;
            } else {
                switchPlayer();
            }
        }
    }
};

int main() {
    char playAgain;
    do {
        TicTacToe game;
        game.play();
        cout << "Do you want to play again? (y/n): ";
        cin >> playAgain;
    } while (playAgain == 'y' || playAgain == 'Y');

    cout << "Thanks for playing!\n";
    return 0;
}

