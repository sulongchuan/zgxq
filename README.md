# zgxq
 Chinese chess
import numpy as np

# 初始化棋盘
board = np.zeros((10, 9), dtype=int)

# 棋子的值
CHE = 1
MA = 2
XIANG = 3
SHI = 4
JIANG = 5
PAO = 6
BING = 7

# 初始化棋子位置
board[0][0] = board[0][8] = CHE
board[0][1] = board[0][7] = MA
board[0][2] = board[0][6] = XIANG
board[0][3] = board[0][5] = SHI
board[0][4] = JIANG
board[2][1] = board[2][7] = PAO
board[3][0] = board[3][2] = board[3][4] = board[3][6] = board[3][8] = BING

# 棋盘坐标转换为象棋位置表示
def get_pos(row, col):
    return chr(ord('a') + col) + str(10 - row)

# 象棋位置表示转换为棋盘坐标
def get_coord(pos):
    col = ord(pos[0]) - ord('a')
    row = 10 - int(pos[1])
    return row, col

# 显示棋盘
def display_board():
    print("  a b c d e f g h i")
    for row in range(10):
        line = str(10 - row) + " "
        for col in range(9):
            if board[row][col] == 0:
                line += ". "
            elif board[row][col] == CHE:
                line += "車"
            elif board[row][col] == MA:
                line += "馬"
            elif board[row][col] == XIANG:
                line += "相"
            elif board[row][col] == SHI:
                line += "仕"
            elif board[row][col] == JIANG:
                line += "将"
            elif board[row][col] == PAO:
                line += "炮"
            elif board[row][col] == BING:
                line += "兵"
            line += " "
        line += str(10 - row)
        print(line)
    print("  a b c d e f g h i")

# 移动棋子
def move_piece(pos1, pos2):
    row1, col1 = get_coord(pos1)
    row2, col2 = get_coord(pos2)
    if board[row2][col2] == JIANG:
        print("游戏结束！")
        return True
    board[row2][col2] = board[row1][col1]
    board[row1][col1] = 0
    return False

# 游戏循环
display_board()
while True:
    pos1 = input("请输入要移动的棋子位置：")
    pos2 = input("请输入目标位置：")
    if move_piece(pos1, pos2):
        break
    display_board()
