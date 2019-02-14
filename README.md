QixBAS is a surving game in which you control the direction of Qix:
- 'A' key to turn it counter-clockwise.
- 'S' key to turn it clockwise.

It loses a bar whenever it collides with the edge of the screen.

It was developed on MSX2 emu on https://webmsx.org/

Instructions:
1) select machine: MSX2++
2) ALT-B
3) paste source code (Qix.bas)
4) RUN

Commented Source Code:
```
10 A =RND(TIME)*3.14:R=10:S=10:X=50:Y=50:L=10:U=10:W=250:H=212:ST=0.2
```
Initialize variables
A: angle of qix direction
R: size of qix bar
S: step size
X,Y: Qix position
L: number of bars
U: maximum bar number


```
20 DIM X1(U-1):DIM X2(U-1):DIM Y1(U-1):DIM Y2(U-1):SCREEN 2
```
X1,X2,Y1,Y2: previous position arrays

```
100 LINE (X1(L-1),Y1(L-1))-(X2(L-1),Y2(L-1)),0 
```
DRAW QIX at position

```
110 KR$ = INKEY$ : if KR$="a" THEN A = A- ST: ELSE IF KR$="s" THEN A = A + ST
```
READ key and change Qix angle direction

```
130 if X>W OR X<0 OR Y<0 OR Y>H THEN A = A+3.14/2 : L=L-1 : if L<2 then L = 2
```
In case of border collision invert direction

```
205 FOR I=L-1 TO 1 STEP-1:X1(I)=X1(I-1):X2(I)=X2(I-1):Y1(I)=Y1(I-1)
```
Shift previous position

```
210 Y2(I)=Y2(I-1):NEXT I:X = X + S*COS(A): Y = Y + S*SIN(A): A1=A -90:A2=A+90:
```
Compute Qix next position

```
220 X1(0)=X+R*COS(A1):Y1(0)=Y+R*SIN(A1):X2(0)=X+R*COS(A2):Y2(0)=Y+R*SIN(A2)
```
Compute actual bar position.

```
230 FOR I =1 TO L-2 : LINE (X1(I),Y1(I))-(X2(I),Y2(I)),1:NEXT I:
```
Draw Qix bars

```
240 LINE (X1(0),Y1(0))-(X2(0),Y2(0)), 2:GOTO 100
```
Draw Qix Actual Bar e loop.

Have fun with QixBAS
