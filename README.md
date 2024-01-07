#include <stdio.h>
#include <stdbool.h>

#define SIZE 8

char chess[SIZE][SIZE] = {
    {'0', '0', '0', '0', '0', '0', '0', '0'},
    {'0', '0', '0', '0', '0', '0', '0', '0'},
    {'0', '0', '0', '0', '0', '0', '0', '0'},
    {'0', '0', '0', '1', '2', '0', '0', '0'},
    {'0', '0', '0', '1', '1', '0', '0', '0'},
    {'0', '0', '0', '1', '0', '0', '0', '0'},
    {'0', '0', '0', '0', '0', '0', '0', '0'},
    {'0', '0', '0', '0', '0', '0', '0', '0'},
};

bool is_valid_position(int x, int y) {
    return x >= 0 && x < SIZE && y >= 0 && y < SIZE;
}

bool find_valid_move(int chess[SIZE][SIZE], int i, int j, int dx, int dy, int *steps) {
    int x = i + dx;
    int y = j + dy;

    if (!is_valid_position(x, y) || chess[i][j] != '0') {
        return false;
    }

    *steps = 0;
    while (is_valid_position(x, y)) {
        if (chess[x][y] == '0') {
            return true;
        }
        x += dx;
        y += dy;
        (*steps)++;
    }

    return false;
}

void print_valid_moves(int chess[SIZE][SIZE]) {
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            if (chess[i][j] == '1') {
                printf("Black piece at (%d,%d):\n", i + 1, j + 1);
                for (int dx = -1; dx <= 1; dx++) {
                    for (int dy = -1; dy <= 1; dy++) {
                        if (dx != 0 || dy != 0) {
                            int steps;
                            if (find_valid_move(chess, i, j, dx, dy, &steps)) {
                                printf("  Direction (%d,%d), steps: %d\n", dx, dy, steps);
                            }
                        }
                    }
                }
            } else if (chess[i][j] == '2') {
                printf("White piece at (%d,%d):\n", i + 1, j + 1);
                for (int dx = -1; dx <= 1; dx++) {
                    for (int dy = -1; dy <= 1; dy++) {
                        if (dx != 0 || dy != 0) {
                            int steps;
                            if (find_valid_move(chess, i, j, dx, dy, &steps)) {
                                printf("  Direction (%d,%d), steps: %d\n", dx, dy, steps);
                            }
                        }
                    }
                }
            }
        }
    }
}

int main() {
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            printf("%c", chess[i][j]);
        }
        printf("\n");
    }

    int i, j;

    while (scanf("%d%d", &i, &j) != EOF) {
        if (i < 0 || j < 0 || i >= SIZE || j >= SIZE) {
            printf("不合法\n");
            continue;
        }

        if (chess[i][j] == '1') {
            printf("黑棋\n");
        } else if (chess[i][j] == '2') {
            printf("白棋\n");
        } else {
            printf("空白\n");
            int steps;
            if (!find_valid_move(chess, i, j, 0, 0, &steps)) {
                printf("沒有位置可以下\n");
            }
        }

        print_valid_moves(chess);
    }

    return 0;
}
