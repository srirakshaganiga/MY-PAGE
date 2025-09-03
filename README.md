#include <stdio.h>
#include <stdlib.h>

char board[3][3];   // 3x3 board

// Function to initialize board
void initBoard() {
    int i, j, pos = 1;
    for (i = 0; i < 3; i++) {
        for (j = 0; j < 3; j++) {
            board[i][j] = '0' + pos; // fill with 1-9
            pos++;
        }
    }
}

// Function to display board
void printBoard() {
    printf("\n");
    for (int i = 0; i < 3; i++) {
        printf(" %c | %c | %c \n", board[i][0], board[i][1], board[i][2]);
        if (i < 2) printf("---|---|---\n");
    }
    printf("\n");
}

// Check winner
int checkWinner() {
    for (int i = 0; i < 3; i++) {
        // Rows
        if (board[i][0] == board[i][1] && board[i][1] == board[i][2]) return 1;
        // Cols
        if (board[0][i] == board[1][i] && board[1][i] == board[2][i]) return 1;
    }
    // Diagonals
    if (board[0][0] == board[1][1] && board[1][1] == board[2][2]) return 1;
    if (board[0][2] == board[1][1] && board[1][1] == board[2][0]) return 1;

    return 0;
}

// Check draw
int isDraw() {
    for (int i = 0; i < 3; i++)
        for (int j = 0; j < 3; j++)
            if (board[i][j] != 'X' && board[i][j] != 'O')
                return 0;
    return 1;
}

int main() {
    int player = 1, choice, row, col;
    char mark;

    initBoard();

    while (1) {
        printBoard();
        mark = (player == 1) ? 'X' : 'O';

        printf("Player %d, enter position (1-9): ", player);
        scanf("%d", &choice);

        // Convert choice into row & col
        row = (choice - 1) / 3;
        col = (choice - 1) % 3;

        // Check valid move
        if (choice < 1 || choice > 9 || board[row][col] == 'X' || board[row][col] == 'O') {
            printf("Invalid move! Try again.\n");
            continue;
        }

        board[row][col] = mark;

        // Check win
        if (checkWinner()) {
            printBoard();
            printf("Player %d WINS! 🎉\n", player);
            break;
        }

        // Check draw
        if (isDraw()) {
            printBoard();
            printf("It's a DRAW!\n");
            break;
        }

        // Switch player
        player = (player == 1) ? 2 : 1;
    }

    return 0;
}


