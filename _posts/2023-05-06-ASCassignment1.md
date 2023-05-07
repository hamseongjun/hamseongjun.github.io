---
layout: single
title: "[ASC 프로그래밍 스터디] 2D MapGame 만들기 (1단계) - Game setup, Cheat map, Quit 구현"
categories: "ASC-Programing_study"
tags: [ASC, 과제, C]
author_profile: false
header:
    teaser: /assets/images/C.png
sidebar:
    nav: "counts"
---
   
![Java]({{site.url}}/assets/images/c-programming.jpg){: .align-center}

<br>

# 개요

ASC 프로그래밍 스터디가 시작되었다.   
오늘은 1주차 스터디가 끝나고 앞으로 스터디 기간 동안 진행될 2D Map Game 만들기 과제 중    
stage1인 게임 초기 세팅과 c, q 커맨드를 구현해보려고 한다.

> cf) 이 글은 2023년 5월 2일에 진행됐던 ASC 프로그래밍 스터디 1주차 스터디 내용을 정리한 글입니다.

# 1. 문제

**컨셉 : 게임의 목표는 플레이어가 맵을 돌아다니며 모든 몬스터를 죽이는 것(회복 포션 기능 제공)**

## 제공된 구조체

- `struct location`   
    - **Purpose:** To store the state of each point on the map.   
    - **Contains:**   
        - `char occupier` - Type of object at this position. Options include:   
            - ‘B’ = Boulder   
            - ‘E’ = Empty   
            - ‘H’ = Healing Potion   
            - ‘M’ = Monster   
            - ‘P’ = Player   
        - `int points` - The health damage/healing the occupier at this map position can inflict. For example   
            - **Points > 0** = Healing   
            - **Points < 0** = Damage   
            
![](https://velog.velcdn.com/images/hamseongjun/post/ee60d6b6-e788-4a83-9bd1-9fc6b07b4892/image.png)


## 기본 틀 코드
```c
// TODO: Description of your program.

#include <stdio.h>

// Additional libraries here


// Provided constants 
#define SIZE 8
#define PLAYER_STARTING_ROW (SIZE - 1)
#define PLAYER_STARTING_COL 0
#define EMPTY_POINTS 0
#define EMPTY_TYPE 'E'
#define PLAYER_TYPE 'P'
#define MONSTER_TYPE 'M'
#define HEALING_TYPE 'H'
#define BOULDER_TYPE 'B'

// Your constants here

// Provided struct
struct location {
    char occupier;
    int points;
};

// Your structs here

// Provided functions use for game setup
// You do not need to use these functions yourself.
void init_map(struct location map[SIZE][SIZE]);
void place_player_on_starting_location(struct location map[SIZE][SIZE]);

// You will need to use these functions for stage 1.
void print_cheat_map(struct location map[SIZE][SIZE]);
void print_game_play_map(struct location map[SIZE][SIZE]);

// Your functions prototypes here

int main(void) {

    struct location map[SIZE][SIZE];
    init_map(map);

    printf("Welcome Explorer!!\n");
    printf("How many game pieces are on the map?\n");
    
    // TODO: Add code to scan in the number of game pieces here.
    
    // TODO: Add code to scan in the details of each game piece and place them
    //       on the map

    // After the game pieces have been added to the map print out the map.
    print_game_play_map(map);
    printf("\nEXPLORE!\n");
    printf("Enter command: ");

    // TODO: keep scanning in commands from the user until the user presses
    // ctrl + d
    
    return 0;
}


////////////////////////////////////////////////////////////////////////////////
///////////////////////////// ADDITIONAL FUNCTIONS /////////////////////////////
////////////////////////////////////////////////////////////////////////////////

// TODO: you may need to add additional functions here

////////////////////////////////////////////////////////////////////////////////
////////////////////////////// PROVIDED FUNCTIONS //////////////////////////////
/////////////////////////// (DO NOT EDIT BELOW HERE) ///////////////////////////
////////////////////////////////////////////////////////////////////////////////

// Provided Function
// Initalises all elements on the map to be empty to prevent access errors.
void init_map(struct location map[SIZE][SIZE]) {
    int row = 0;
    while (row < SIZE) {
        int col = 0;
        while (col < SIZE) {
            struct location curr_loc;
            curr_loc.occupier = EMPTY_TYPE;
            curr_loc.points = EMPTY_POINTS;
            map[row][col] = curr_loc;
            col++;
        }
        row++;
    }

    place_player_on_starting_location(map);
}

// Provided Function
// Places the player in the bottom left most location.
void place_player_on_starting_location(struct location map[SIZE][SIZE]) {
    map[PLAYER_STARTING_ROW][PLAYER_STARTING_COL].occupier = PLAYER_TYPE;
}

// Provided Function
// Prints out map with alphabetic values. Monsters are represented with 'M',
// healing potions in 'H', boulders with 'B' and the player with 'P'.
void print_game_play_map(struct location map[SIZE][SIZE]) {
    printf(" -----------------\n");
    int row = 0;
    while (row < SIZE) {
        printf("| ");
        int col = 0;
        while (col < SIZE) {
            if (map[row][col].occupier == EMPTY_TYPE) {
                printf("- ");
            } else {
                printf("%c ", map[row][col].occupier);
            }
            col++;
        }
        printf("|\n");
        row++;
    }
    printf(" -----------------\n");
}

// Provided Function
// Prints out map with numerical values. Monsters are represented in red,
// healing potions in blue, boulder in green and the player in yellow.
//
// We use some functionality you have not been taught to make sure that
// colours do not appear during testing.
void print_cheat_map(struct location map[SIZE][SIZE]) {

    printf(" -----------------\n");
    int row = 0;
    while (row < SIZE) {
        printf("| ");
        int col = 0;
        while (col < SIZE) {
            if (map[row][col].occupier == PLAYER_TYPE) {
                // print the player in purple
                // ----------------------------------------
                // YOU DO NOT NEED TO UNDERSTAND THIS CODE.
                #ifndef NO_COLORS
                printf("\033[1;35m");
                #endif
                // ----------------------------------------
                printf("%c ", PLAYER_TYPE);
            } else if (map[row][col].occupier == HEALING_TYPE) {
                // print healing potion in green
                // ----------------------------------------
                // YOU DO NOT NEED TO UNDERSTAND THIS CODE.
                #ifndef NO_COLORS
                printf("\033[1;32m");
                #endif
                // ----------------------------------------
                printf("%d ", map[row][col].points);
            } else if (map[row][col].occupier == MONSTER_TYPE) {
                // print monsters in red
                // ----------------------------------------
                // YOU DO NOT NEED TO UNDERSTAND THIS CODE.
                #ifndef NO_COLORS
                printf("\033[1;31m");
                #endif
                // ----------------------------------------
                printf("%d ", -map[row][col].points);
            } else if (map[row][col].occupier == BOULDER_TYPE) {
                // print boulder in blue
                // ----------------------------------------
                // YOU DO NOT NEED TO UNDERSTAND THIS CODE.
                #ifndef NO_COLORS
                printf("\033[1;34m");
                #endif
                // ----------------------------------------
                printf("%d ", map[row][col].points);
            } else {
                // print empty squares in the default colour
                printf("- ");
            }
            // ----------------------------------------
            // YOU DO NOT NEED TO UNDERSTAND THIS CODE.
            // reset the colour back to default
            #ifndef NO_COLORS
            printf("\033[0m");
            #endif
            // ----------------------------------------
            col++;
        }
        printf("|\n");
        row++;
    }
    printf(" -----------------\n");
}
```


## 다음 기능으로만 구현하기

- int, char 변수   
- if문    
- while문   
- printf, scanf   
- 구조체   
- 배열(1차원, 2차원)   


## 구현 목표

| Stage | Command Name | Example | Meaning |
| --- | --- | --- | --- |
| Stage 1.2 | c | c | Print cheat map |
| Stage 1.3 | q | q | Quit the game |
| Stage 2.1 | m [direction] | m r | Move the player |
| Stage 2.2 | h | h | Print out the player’s health |
| Stage 2.5 | s [row] [col] [size] [type] | s 2 3 4 M | Prints out the number of points in a given square |
| Stage 3.3 | b [row] [col] | b 5 5 | Place a boulder at the coordinates |
| Stage 3.4 | r [start_row] [start_col] [end_row] [end_col] [type] | r 1 1 2 2 M | Count points in a box |
| Stage 4.1 | n [size] | n 3 | Print out next step hint |
| Stage 4.2 | a | a | Monster attack |

***

## 📌Stage 1

1. 게임을 시작하기 위해 게임 조각의 수, 유형 및 힘을 선택하는 기능
2. 게임 플레이 맵을 출력하는 기능
3. 치트 맵을 인쇄하는 기능
4. 게임을 종료하는 기능

### 1.1 Game setup 구현

1단계에서는 모든 관련 게임 조각으로 게임 맵을 설정합니다. 또한 사용자에게 지도를 표시합니다.

**명령어**
```c
How many game pieces are on the map? [num pieces] 
    
      [points] [row] [col]
      ... <num pieces times > ...
      [points] [row] [col]
```

**개요**

1. 얼마나 많은 게임 말을 놓을 것인지 묻습니다.   
2. 배치할 게임 말의 수 n을 읽습니다.   
3. n개의 `[points] [row] [col]` ← 입력받는다.    

**pieces 조건(📌 #define에 정의된 것 사용하기!)**

- `points`가 음수   
    - monster이며, `struct location`의 occupier를 ‘M’으로 저장, `[points]` 는 monster의 데미지   
- `points`가 양수   
    - healing potion이며, `struct location` 의 occupier를 ‘H’로 저장, `[points]`는 회복 양   
- `points`가 0   
    - boulder(바위)이며, `struct location` 의 occupier를 ‘B’라고 저장, 바위는 데미지나 회복 x   
    
**설명**

- 플레이어가 지도의 (7, 0) 위치에 자동으로 배치됩니다. init_map함수에서 초기화함   
- 8x8 맵에서 해당 row, col을 벗어나면 안됨(조건)   
- 게임 말의 damage/healing point가 -9~9 범위를 벗어나면 안됨. 벗어나면 해당 줄은 무시하고 지도에 배치 x   
- 플레이어 좌표(7, 0)위치에 다른 말을 둘 수 없고, (7, 0) 좌표에 입력되면 해당 줄은 무시하고 지도에 배치 x   
- 새로운 말이 기존 게임 피스의 좌표가 지정되면 새 말이 맵에 배치되고 기존 말은 더 이상 맵에 없어져야함   
  
#### 예시 1.1.1(게임 말 입력)

- (2,3)위치에 1개의 돌   
- (4,7)위치에 1개의 몬스터   
- (6,4)위치에 1개의 회복 포션   

```
./2d-mapgame
Welcome Explorer!!
How many game pieces are on the map? 
3
Enter the details of game pieces:
0 2 3
-6 4 7
3 6 4
 -----------------
| - - - - - - - - |
| - - - - - - - - |
| - - - B - - - - |
| - - - - - - - - |
| - - - - - - - M |
| - - - - - - - - |
| - - - - H - - - |
| P - - - - - - - |
 -----------------

EXPLORE!
```

#### 예시 1.1.2(잘못된 입력)
```
./2d-mapgame
Welcome Explorer!!
How many game pieces are on the map? 
4
Enter the details of game pieces:
0 2 8
-3 5 1
11 3 6
-2 4 -14
 -----------------
| - - - - - - - - |
| - - - - - - - - |
| - - - - - - - - |
| - - - - - - - - |
| - - - - - - - - |
| - M - - - - - - |
| - - - - - - - - |
| P - - - - - - - |
 -----------------

./cs_explorer
Welcome Explorer!!
How many game pieces are on the map? 
1
Enter the details of game pieces:
-3 7 0
 -----------------
| - - - - - - - - |
| - - - - - - - - |
| - - - - - - - - |
| - - - - - - - - |
| - - - - - - - - |
| - - - - - - - - |
| - - - - - - - - |
| P - - - - - - - |
 -----------------
 ```
 
### 1.2 Cheat Map 구현   

 `c` 명령이 입력되면 `print_cheat_map` 함수를 호출

- red numbers = monsters   
- green numbers = healing potions   
- blue zero's = boulders   
- purple 'P' = the player   

#### 예시 1.2.1(Cheat Map 예시)
```
./2d-mapgame
Welcome Explorer!!
How many game pieces are on the map?
3
Enter the details of game pieces:
0 2 3
-6 4 7
3 6 4
 -----------------
| - - - - - - - - |
| - - - - - - - - |
| - - - B - - - - |
| - - - - - - - - |
| - - - - - - - M |
| - - - - - - - - |
| - - - - H - - - |
| P - - - - - - - |
 -----------------

EXPLORE!
Enter command: c
 -----------------
| - - - - - - - - |
| - - - - - - - - |
| - - - 0 - - - - |
| - - - - - - - - |
| - - - - - - - 6 |
| - - - - - - - - |
| - - - - 3 - - - |
| P - - - - - - - |
 -----------------

 -----------------
| - - - - - - - - |
| - - - - - - - - |
| - - - B - - - - |
| - - - - - - - - |
| - - - - - - - M |
| - - - - - - - - |
| - - - - H - - - |
| P - - - - - - - |
 -----------------
 ```
 
### 1.3 Quit 구현

`q` 명령어가 입력되면 `Exiting Program!` 를 출력하고, `exit()` 함수를 이용해서 프로그램 종료

#### 예시 1.3.1(Quit 예시)
```
./2d-mapgame
Welcome Explorer!!
How many game pieces are on the map?
1
Enter the details of game pieces:
5 4 4
 -----------------
| - - - - - - - - |
| - - - - - - - - |
| - - - - - - - - |
| - - - - - - - - |
| - - - - H - - - |
| - - - - - - - - |
| - - - - - - - - |
| P - - - - - - - |
-----------------

EXPLORE!
Enter command: c
 -----------------
| - - - - - - - - |
| - - - - - - - - |
| - - - - - - - - |
| - - - - - - - - |
| - - - - 5 - - - |
| - - - - - - - - |
| - - - - - - - - |
| P - - - - - - - |
 -----------------
 -----------------
| - - - - - - - - |
| - - - - - - - - |
| - - - - - - - - |
| - - - - - - - - |
| - - - - H - - - |
| - - - - - - - - |
| - - - - - - - - |
| P - - - - - - - |
 -----------------
Enter command: q
Exiting Program!
```

***

# 코드

예시 틀 코드를 잘 보면 주석문으로 `//TODO: ...` 라고 적힌 부분이 있다.   
틀 코드에 필요한 함수 기능이 다 구현되어 있기 때문에 main에서 TODO 부분에만 코드를 잘 넣어주면 될 것 같다.   

## 구현한 코드

```c
int main(void) {

    struct location map[SIZE][SIZE];
    init_map(map);

    printf("Welcome Explorer!!\n");
    printf("How many game pieces are on the map?\n");
    
    // TODO: Add code to scan in the number of game pieces here.
    int n;
    scanf("%d", &n);
    // TODO: Add code to scan in the details of each game piece and place them
    //       on the map
    int points, row, col;
    for(int i = 0; i < n; i++){      //Repeat n times.
        if(i == 0){
            printf("Enter the details of game pieces:\n");
            printf("[points] [row] [col]\n");
        }                   
        scanf(" %d %d %d", &points, &row, &col);
        if(row < 0 || row > (SIZE-1)
        || col < 0 || col > (SIZE-1)
        || points < MIN_POINT || points > MAX_POINT
        || (row == PLAYER_STARTING_ROW && col == PLAYER_STARTING_COL)) {    //invalid input
            continue;
        }
        else if(points < 0) {     //monster
            map[row][col].occupier = MONSTER_TYPE;
            map[row][col].points = points;
        }
        else if(points > 0) {    //healing potion
            map[row][col].occupier = HEALING_TYPE;
            map[row][col].points = points;
        }
        else {  //boulder
            map[row][col].occupier = BOULDER_TYPE;
            map[row][col].points = EMPTY_POINTS;
        }
    }
            
    // After the game pieces have been added to the map print out the map.
    print_game_play_map(map);
    printf("\nEXPLORE!\n");
    printf("Enter command: ");

    // TODO: keep scanning in commands from the user until the user presses
    // ctrl + d
    char command;
    while(1){
        scanf(" %c", &command);
        
        if(command == 'c') {    //Cheat Map
            print_cheat_map(map);
            printf("\n");
        }
        else if(command == 'q') {//Quit
            printf("Exiting Program!\n");
            break;
        }

        print_game_play_map(map);
        printf("Enter command: ");
    }
    return 0;
}
```

## 전체 코드

```c
// TODO: Description of your program.

#include <stdio.h>

// Additional libraries here


// Provided constants 
#define SIZE 8
#define PLAYER_STARTING_ROW (SIZE - 1)
#define PLAYER_STARTING_COL 0
#define EMPTY_POINTS 0
#define EMPTY_TYPE 'E'
#define PLAYER_TYPE 'P'
#define MONSTER_TYPE 'M'
#define HEALING_TYPE 'H'
#define BOULDER_TYPE 'B'

// Your constants here

// Provided struct
struct location {
    char occupier;
    int points;
};

// Your structs here
#define MIN_POINT -9
#define MAX_POINT 9
// Provided functions use for game setup
// You do not need to use these functions yourself.
void init_map(struct location map[SIZE][SIZE]);
void place_player_on_starting_location(struct location map[SIZE][SIZE]);

// You will need to use these functions for stage 1.
void print_cheat_map(struct location map[SIZE][SIZE]);
void print_game_play_map(struct location map[SIZE][SIZE]);

// Your functions prototypes here

int main(void) {

    struct location map[SIZE][SIZE];
    init_map(map);

    printf("Welcome Explorer!!\n");
    printf("How many game pieces are on the map?\n");
    
    // TODO: Add code to scan in the number of game pieces here.
    int n;
    scanf("%d", &n);
    // TODO: Add code to scan in the details of each game piece and place them
    //       on the map
    int points, row, col;
    for(int i = 0; i < n; i++){      //Repeat n times.
        if(i == 0){
            printf("Enter the details of game pieces:\n");
            printf("[points] [row] [col]\n");
        }                   
        scanf(" %d %d %d", &points, &row, &col);
        if(row < 0 || row > (SIZE-1)
        || col < 0 || col > (SIZE-1)
        || points < MIN_POINT || points > MAX_POINT
        || (row == PLAYER_STARTING_ROW && col == PLAYER_STARTING_COL)) {    //invalid input
            continue;
        }
        else if(points < 0) {     //monster
            map[row][col].occupier = MONSTER_TYPE;
            map[row][col].points = points;
        }
        else if(points > 0) {    //healing potion
            map[row][col].occupier = HEALING_TYPE;
            map[row][col].points = points;
        }
        else {  //boulder
            map[row][col].occupier = BOULDER_TYPE;
            map[row][col].points = EMPTY_POINTS;
        }
    }
            
    // After the game pieces have been added to the map print out the map.
    print_game_play_map(map);
    printf("\nEXPLORE!\n");
    printf("Enter command: ");

    // TODO: keep scanning in commands from the user until the user presses
    // ctrl + d
    char command;
    while(1){
        scanf(" %c", &command);
        
        if(command == 'c') {    //Cheat Map
            print_cheat_map(map);
            printf("\n");
        }
        else if(command == 'q') {//Quit
            printf("Exiting Program!\n");
            break;
        }

        print_game_play_map(map);
        printf("Enter command: ");
    }
    return 0;
}


////////////////////////////////////////////////////////////////////////////////
///////////////////////////// ADDITIONAL FUNCTIONS /////////////////////////////
////////////////////////////////////////////////////////////////////////////////

// TODO: you may need to add additional functions here

////////////////////////////////////////////////////////////////////////////////
////////////////////////////// PROVIDED FUNCTIONS //////////////////////////////
/////////////////////////// (DO NOT EDIT BELOW HERE) ///////////////////////////
////////////////////////////////////////////////////////////////////////////////

// Provided Function
// Initalises all elements on the map to be empty to prevent access errors.
void init_map(struct location map[SIZE][SIZE]) {
    int row = 0;
    while (row < SIZE) {
        int col = 0;
        while (col < SIZE) {
            struct location curr_loc;
            curr_loc.occupier = EMPTY_TYPE;
            curr_loc.points = EMPTY_POINTS;
            map[row][col] = curr_loc;
            col++;
        }
        row++;
    }

    place_player_on_starting_location(map);
}

// Provided Function
// Places the player in the bottom left most location.
void place_player_on_starting_location(struct location map[SIZE][SIZE]) {
    map[PLAYER_STARTING_ROW][PLAYER_STARTING_COL].occupier = PLAYER_TYPE;
}

// Provided Function
// Prints out map with alphabetic values. Monsters are represented with 'M',
// healing potions in 'H', boulders with 'B' and the player with 'P'.
void print_game_play_map(struct location map[SIZE][SIZE]) {
    printf(" -----------------\n");
    int row = 0;
    while (row < SIZE) {
        printf("| ");
        int col = 0;
        while (col < SIZE) {
            if (map[row][col].occupier == EMPTY_TYPE) {
                printf("- ");
            } else {
                printf("%c ", map[row][col].occupier);
            }
            col++;
        }
        printf("|\n");
        row++;
    }
    printf(" -----------------\n");
}

// Provided Function
// Prints out map with numerical values. Monsters are represented in red,
// healing potions in blue, boulder in green and the player in yellow.
//
// We use some functionality you have not been taught to make sure that
// colours do not appear during testing.
void print_cheat_map(struct location map[SIZE][SIZE]) {

    printf(" -----------------\n");
    int row = 0;
    while (row < SIZE) {
        printf("| ");
        int col = 0;
        while (col < SIZE) {
            if (map[row][col].occupier == PLAYER_TYPE) {
                // print the player in purple
                // ----------------------------------------
                // YOU DO NOT NEED TO UNDERSTAND THIS CODE.
                #ifndef NO_COLORS
                printf("\033[1;35m");
                #endif
                // ----------------------------------------
                printf("%c ", PLAYER_TYPE);
            } else if (map[row][col].occupier == HEALING_TYPE) {
                // print healing potion in green
                // ----------------------------------------
                // YOU DO NOT NEED TO UNDERSTAND THIS CODE.
                #ifndef NO_COLORS
                printf("\033[1;32m");
                #endif
                // ----------------------------------------
                printf("%d ", map[row][col].points);
            } else if (map[row][col].occupier == MONSTER_TYPE) {
                // print monsters in red
                // ----------------------------------------
                // YOU DO NOT NEED TO UNDERSTAND THIS CODE.
                #ifndef NO_COLORS
                printf("\033[1;31m");
                #endif
                // ----------------------------------------
                printf("%d ", -map[row][col].points);
            } else if (map[row][col].occupier == BOULDER_TYPE) {
                // print boulder in blue
                // ----------------------------------------
                // YOU DO NOT NEED TO UNDERSTAND THIS CODE.
                #ifndef NO_COLORS
                printf("\033[1;34m");
                #endif
                // ----------------------------------------
                printf("%d ", map[row][col].points);
            } else {
                // print empty squares in the default colour
                printf("- ");
            }
            // ----------------------------------------
            // YOU DO NOT NEED TO UNDERSTAND THIS CODE.
            // reset the colour back to default
            #ifndef NO_COLORS
            printf("\033[0m");
            #endif
            // ----------------------------------------
            col++;
        }
        printf("|\n");
        row++;
    }
    printf(" -----------------\n");
}
```

***

# 후기

처음에 과제 명세 페이지 맨 아래에 stage1에 대한 설명이 담긴 링크가 있는지 모르고 문제를 풀기 시작했어 가지고 정말 막막했다.

혹시라도 다른 동아리원 중에 코드를 올린 사람이 있을까 싶어서 깃허브에 들어가서 뒤져보니 제대로 만든 사람이 1명도 없었다. (애초에 제출한 사람이 2명...)

그렇게 google 이미지 검색으로 해당 과제의 원본 영문 페이지에 들어가서 페이지 번역을 하면서 문제를 풀려니까 이건 도저히 아닌 것 같아서 과제 명세 페이지를 다시 살펴보니 stage1 명세 링크를 그제서야 발견했다...

아무튼 뼈대 코드에 구조체 배열인 map도 잘 선언했고, stage1에서 사용할 print_cheat_map()과 print_game_play_map()이 이미 구현이 되어 있어서, 어려울 건 전혀 없었다.   

내가 구현한 부분은 if문으로 조건만 잘 맞춰서 논리 문장만 잘 적어주기만 하면 끝나는 문제였다.

논리 연산은 1학년 1학기 떄 시험 공부 때문에 주구장창 공부했던 거라 이 정도는 가뿐했다. ~~(ㄱㅇㅅ 그는 도대체...)~~

뭔가 조금 조잡하긴 하지만, 제대로 된 게임을 만드는 것 같아서 과제 만드는 과정이 정말 재밌었던 것 같다.

과제를 다 만들고 나서 깃허브에 push 한 후에 다른 사람들이 만든 코드와 내가 만든 코드를 비교해보려고 다른 사람들 레포를 봤더니 아직까지도 제대로 구현해서 올린 사람이 1명도 없다. 내가 제일 빨리 제출한 듯 하다.   
(이틀 뒤에 2주차 시작하는데 어떡하려고 그러냐...)

앞으로 남은 스터디와 과제도 힘내서 파이팅하자. 아자아자! ╰(*°▽°*)╯