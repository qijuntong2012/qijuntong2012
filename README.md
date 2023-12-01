```
#include<bits/stdc++.h>
#include<cstdlib>
#include<ctime>
#include<Windows.h>
#define int long long
#define f(i,j,k) for(int i=j;i<=k;i++)
#define rf(i,j,k) for(int i=j;i>=k;i--)
#define mm(i) memset(i,0,sizeof i)
#define rm(i) memset(i,0x3f,sizeof i)
using namespace std;
const int N=1e5+5;
const double pi=acos(-1.0);
const int BUFFER_SIZE=50;
const int RAIN_LENGTH=18;
int WIDTH=80;
int HEIGHT=30;
typedef struct{
    int x,y;
    char ch;
}RAINDROP;
RAINDROP raindropLine[BUFFER_SIZE];
HANDLE HOUT=GetStdHandle(STD_OUTPUT_HANDLE);
void gotoxy(int x,int y){
    COORD pos;
    pos.X=x;
    pos.Y=y;
    SetConsoleCursorPosition(HOUT, pos);
}
void show_cursor(BOOL hide){
    CONSOLE_CURSOR_INFO cciCursor;
    if(GetConsoleCursorInfo(HOUT,&cciCursor)){
        cciCursor.bVisible=hide;
        SetConsoleCursorInfo(HOUT,&cciCursor);
    }
}
void set_color(int color){
    SetConsoleTextAttribute(HOUT,color);
}
signed main(){
//	freopen(".in","r",stdin);
//	freopen(".out","w",stdout);
	ios::sync_with_stdio(false);
	cin.tie(0);
	cout.tie(0);
	CONSOLE_SCREEN_BUFFER_INFO info;
    GetConsoleScreenBufferInfo(HOUT,&info);
    HEIGHT=info.srWindow.Bottom;
    WIDTH=info.srWindow.Right;
    show_cursor(FALSE);
    srand((unsigned int)time(NULL));
    for(int i=0;i<BUFFER_SIZE;i++){
        raindropLine[i].x=rand()%WIDTH;
        raindropLine[i].y=rand()%HEIGHT;
        raindropLine[i].ch='0'+rand()%2;
    }
    while(true){
        GetConsoleScreenBufferInfo(HOUT,&info);
        HEIGHT=info.srWindow.Bottom;
        WIDTH=info.srWindow.Right;
        for(int i=0;i<BUFFER_SIZE;++i){
            if(raindropLine[i].y<=HEIGHT){
                gotoxy(raindropLine[i].x,raindropLine[i].y);
                set_color(FOREGROUND_GREEN);
                putchar(raindropLine[i].ch);
            }
            gotoxy(raindropLine[i].x,raindropLine[i].y-RAIN_LENGTH);
            putchar(' ');
            raindropLine[i].y++;
            raindropLine[i].ch='0'+rand()%2;
            if(raindropLine[i].y>HEIGHT+RAIN_LENGTH){
                raindropLine[i].x=rand()%WIDTH;
                raindropLine[i].y=rand()%HEIGHT;
            }
            if(raindropLine[i].y<=HEIGHT){
                gotoxy(raindropLine[i].x,raindropLine[i].y);
                set_color(FOREGROUND_GREEN|FOREGROUND_INTENSITY);
                putchar(raindropLine[i].ch);
            }
        }
        Sleep(30);
    }
    getchar();
//	fclose(stdin);
//	fclose(stdout);
	return 0;
}
```
