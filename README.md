#include <windows.h> 
#include <iostream> 
#include <conio.h> 
#include <math.h> 
using namespace std;

void draw_line(int t1_x, int t1_y, int t2_x, int t2_y){ 
 HWND hwnd = GetConsoleWindow(); 
 HDC hdc = GetDC(hwnd); 
  
 const int deltaX = abs(t2_x - t1_x);//size for x, wight
 const int deltaY = abs(t2_y - t1_y);//size for y, hight 
 const int X_way = t1_x < t2_x ? 1 : -1;//x go right(1) or left(-1)
 const int Y_way = t1_y < t2_y ? 1 : -1; //y go up(1) or down(-1)
 int deltXY = deltaX - deltaY;
 while (t1_x != t2_x || t1_y != t2_y){//while point not at the end
    SetPixel(hdc, t1_x, t1_y, RGB(255, 255, 255));//draw pixel xy
    const int deltXY2 = deltXY * 2;//fix brethenhem
    if (deltXY2 < deltaX){
        deltXY += deltaX; //move x to the way
        t1_y += Y_way;//move y to the way
    }
    if (deltXY2 > -deltaY){
        deltXY -= deltaY;//move y down
        t1_x += X_way;//move point x right
    }
} 
  
 ReleaseDC(hwnd, hdc); 
}
void show_crkl(int Ox, int Oy, int RD){//central point
 HWND hwnd = GetConsoleWindow(); 
 HDC hdc = GetDC(hwnd);
 int DM = RD*2,x = RD-1,y = 0,tx = 1, ty = 1,CORRECT = tx - DM;//for drawing
 //diametr,xy points, xy move, correction
 while(x>=y){
 	SetPixel(hdc,Ox+x,Oy-y,RGB(255,255,0));SetPixel(hdc,Ox+x,Oy+y,RGB(255,255,0));
 	SetPixel(hdc,Ox-x,Oy-y,RGB(255,255,0));SetPixel(hdc,Ox-x,Oy+y,RGB(255,255,0));
 	SetPixel(hdc,Ox+y,Oy-x,RGB(255,255,0));SetPixel(hdc,Ox+y,Oy+x,RGB(255,255,0));
 	SetPixel(hdc,Ox-y,Oy-x,RGB(255,255,0));SetPixel(hdc,Ox-y,Oy+x,RGB(255,255,0));
 	if(CORRECT<=0){y++;CORRECT+=ty;ty+=2;}//make an edits for correction
	if(CORRECT>0){x--;tx+=2;CORRECT+=tx-DM;}//another corrections for quadrants
 }
 //basic algorytm for cyrcle from central point
 ReleaseDC(hwnd, hdc); 
} 
void draw_rect(int x, int y, int right, int down){
	draw_line(x, y, x+right, y); 
 	draw_line(x+right,y,x+right,y+down); 
 	draw_line(x+right,y+down,x,y+down); 
 	draw_line(x,y+down,x,y); 
}
 
int main() 
{ 
 show_crkl(500,500,400);
 draw_rect(100,100,800,800);
  
 _getch(); 
 return 0; 
}

