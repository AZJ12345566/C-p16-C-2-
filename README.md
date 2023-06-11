# C-p16-C-2-
C语言学习笔记 p16 C语言实现三子棋(2)
//test.c源文件部分的代码
#include<stdio.h>
#include<game.h>
void menu()
{
    printf("*********************************\n");
    printf("*******1.play.   0.exit  ********\n");
    printf("*********************************\n");
}

//游戏的整个实现过程
void game()
{
    char ret=0;
    //创建一个数组，存放棋盘信息
    char board[ROW][COL]={0};//数组内容全部空格,因此要初始化
    //初始化棋盘
    InitBoard(board, ROW,COL);
    //打印棋盘
    DisplayBoard(board,ROW,COL);
    //下棋
    while(1)
    {
        //玩家下棋
        PlayerMove(board,ROW,COL);
        DisplayBoard(board,ROW,COL);
        //判断玩家是否赢
        ret=IsWin(board,ROW,COL);
        if(ret!='C')
        {
            break;
        }
        //电脑下棋
        ComputerMove(board,ROW,COL);
        DisplayBoard(board,ROW,COL);
        //判断电脑是否赢
        ret=IsWin(board,ROW,COL);
        if(ret!='C')
        {
            break;
        }
    }
    if(ret=='*')
    {
        printf("玩家赢\n");
    }
    else if(ret=='#')
    {
        printf("电脑赢\n");
    }
    else
    {
        printf("平局\n");
    }
}
void test()
{
    int input=0;
    srand((unsigned int)time(NULL));
    do
    {
        menu();
        printf("请选择:>")
        scanf("%d",&input);
        switch(input)
        {
            case 1:
                //游戏得实现过程
                game();
                break;
            case 0:
                printf("退出游戏\n");
                break;
            default:
                printf("选择错误，请重新选择\n");
                break;
        }
    }while(input);
}
int main()
{
    test();
    return 0;
}




//game.h头文件函数声明代码部分
#define ROW 3
#define COL 3

#include<stdio.h>
#include<stdlib.h>
$include<time.h>
//声明
void InitBoard(int board[ROW][COL],int row,int col);
DisplayBoard(char board[ROW][COL],int row,int col);
PlayerMove(char board[ROW][COL],int row,int col);
ComputerMove(char board[ROW][COL],int row,int col);

//告诉我们四种游戏的状态
//玩家赢-'*'
//电脑赢-'#'
//平局-'Q'
//游戏继续-'C'
char IsWin()

char IsWin(char board[ROW][COL]),int row,int col);



//game.c函数实现部分代码
#include"game.h"
void InitBoard(int board[ROW][COL],int row,int col)
{
    int i=0;
    int j=0;
    for(i=0;i<row;i++)
    {
        for(j=0;j<col;j++)
        {
            board[i][j]=' ';
        }
    }
}

DisplayBoard(char board[ROW][COL],int row,int col);
{
    int i=0;
    for(i=0;i<row;i++)
    {
        //1.打印一行的数据
        printf(" %c | %c | %c \n",board[i][0],board[i][1],board[i][2]);//实现列的时候泛用性太差
        //2.打印分割行
        if(i<row-1)
            printf("---|---|---\n");
    }
}

//优化版本
DisplayBoard(char board[ROW][COL],int row,int col);
{
    int i=0;
    for(i=0;i<row;i++)
    {
        //1.打印一行的数据
        int j=0;
        for(j=0;j<col;j++)
        {
            printf(" %c ",board[i][j]);
            if(j<col-1)
                printf("|");
        }
        printf("\n");
        //2.打印分割行
        if(i<row-1)
        {
            for(j=0;j<col;j++)
            {
                printf("---");
                if(j<col-1)
                    printf("|");
            }
            printf("\n");
        }
    }
}

void PlayerMove(char board[ROW][COL],int row,int col)
{
    int x=0;
    int y=0;
    printf("玩家走:>\n");
    while(1)
    {
        printf("请输入要下的坐标:>");
        scanf("%d%d"&x&y);
        //判断x，y坐标的合法性
        if(x>=1 && x<=row && y>=1 && y<=col)
        {
            if(board(x-1)(y-1)==' ')
            {
                board(x-1)(y-1)='*';
                break;
            }
            else
            {
                printf("该坐标被占用\n");
            }
        }
        else
        {
            printf("坐标非法，重新输入：\n");
        }
    }
}

void ComputerMove(char board[ROW][COL],int row,int col)
{
    int x=0;
    int y=0;
    prnitf("电脑走：>");
    while(1)
    {
        x=rand()%row;
        y=rand()%col;
        if(board[x][y]==' ')
        {
            board[x][y]='*';
            breaak;
        }
    }
}

//返回1表示棋盘满了
//返回0表示棋盘没满
int IsFull(char board[ROW][COL],int row,int col)
{
    int i=0;
    int j=0;
    for(i=0;i<row;i++)
    {
        for(j=0;j<col;j++)
        {
            if(board[i][j]==' ')
            {
                return 0;//没满
            }
        }
    }
    return 1;//满了
}
char IsWin(char board[ROW][COL]),int row,int col)
{
    int i=0;
    //横三行判断输赢
    for(i=0;i<row;i++)
    {
        if(board[i][0]==board[i][1]) && board[i][1]==board[i][2] && board[i][1] != ' ')
        {
            return board[i][1];
        }
    }
    //数三列判断输赢
    for(i=0;i<col;i++)
    {
        if(board[0][1]==board[1][i] && board[1][i]==board[2][i] && board[1][i]!=' ')
        {
            return board[1][i];
        }
    }
    //两个对角线判断输赢
    if(board[0][0]==board[1][1] && board[1][1]==board[2][2] && board[1][1] !=' ')
        return board[1][1];
    if(board[2][0]==board[1][1] && board[1][1]==board[0][2] && board[1][1] !=' ')
        return board[1][1];
    //判断是否平局
    if(1==IsFull(board,ROW,COL))
    {
        return 'Q';
    }
    return 'C';
}


