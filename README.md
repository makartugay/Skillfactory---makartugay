maps = [[".", ".", "."], [".", ".", "."], [".", ".", "."]]
Coord = [0, 0]
Game_over = False
player_1 = True
Symbol = "X"
def check_win(win):
    win_Coord = (((0, 0), (0, 1), (0, 2)), ((1, 0), (1, 1), (1, 2)), ((2, 0), (2, 1), (2, 2)),
                ((0, 2), (1, 1), (2, 0)), ((0, 0), (1, 1), (2, 2)), ((0, 0), (1, 0), (2, 0)),
                ((0, 1), (1, 1), (2, 1)), ((0, 2), (1, 2), (2, 2)))
    for Coord in win_Coord:
        symbols = []
        for c in Coord:
            symbols.append(maps[c[0]][c[1]])
        if symbols == ["X", "X", "X"]:
            print("Выиграл X!!!")
            return True
        if symbols == ["O", "O", "O"]:
            print("Выиграл O!!!")
            return True
    return False
def print_maps():
    for i in maps:
        print(*i)
def step_maps(symbol, coord):
    maps[coord[0]][coord[1]] = symbol
def check_coords(coords: list) -> bool:
    """Проверка координат"""
    if not (coords[0].isdigit() and coords[1].isdigit()):
        return False
    return True
win = "."

while not Game_over:
    print_maps()
    if player_1:
        Symbol = "X"
    else:
        Symbol = "O"
    Coord = [i for i in input("Введите координаты клетки через пробел: ").split()]

    while not check_coords(Coord):
        print("НЕВЕРНЫЕ КООРДИНАТЫ")
        Coord = [i for i in input("Введите координаты клетки через пробел: ").split()]

    while maps[int(Coord[0])][int(Coord[1])] in "OX":
        print("Позиция занята")
        Coord = [i for i in input("Введите координаты клетки через пробел: ").split()]

    step_maps(Symbol, list(map(int, Coord)))
    Game_over = check_win(win)
    player_1 = not player_1

print("Победил игрок 1" if Symbol == "X" else "Победил игрок 2")
