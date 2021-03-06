Lab №1. Simple cycles
--------------------
***
#### Task:
![The task](https://i.imgur.com/dhHKQEz.jpg)

>The program calculates the value of the function from the initial value x **(xn)** to the final value **(xk)** with step **dx**

**Language**: Delphi

**Code:**
``` pascal
program lab1;
{$APPTYPE CONSOLE}
uses
  SysUtils, Windows,  math;

var xn, xk, dx, e, x, y: real;

procedure getY(x: real);
begin
  if((x <= 0) or (pi*pi - x*x + 1/x = 0)) then
    writeln('For x = ', x:0:4, ' the value of the function is not defined')
  else
  begin
    y:=pi*pi - x*x + 1/x;

    if(y<0) then
    begin
      y:=(-1)*Power(abs(y), 1/3);
    end

    else 
    begin
        y:=Power(y, 1/3); 
    end;

    y:= Log10(x)/y;
    y:= y + Power(abs(1.5 - x*x), 1/2)*Tan((x-1)/x);
    writeln('x = ', x:0:4, '; y = ', y:0:4);
  end;
end;

begin


repeat
  writeln('Enter the initial value of x');
  readln(xn);
  writeln('Enter the final value of x');
  readln(xk);
  writeln('Enter a step');
  readln(dx);
  if ((xn>xk) and (dx >= 0))
     or
     ((xn<xk) and (dx <= 0)) then
  begin
    writeln; // 
    writeln; //
    writeln('Incorrect data entered. Please, try again');
    writeln; //
    writeln; //
  end;
until ((xn<=xk) and (dx > 0))
      or
      ((xn>=xk) and (dx < 0));

e:=dx/1000; // Accuracy of machine
x:=xn;
while(((x < xk + e) and (dx > 0))
     or
     ((x > xk + e) and (dx < 0))) do
begin
  getY(x);
  x:= x + dx;
end;


// Checking whether the value of the function for xk
if(((x - dx + e - xk < 0) and (dx > 0))
  or
  ((xk - (x - dx + e) < 0) and (dx < 0))) then
begin
  getY(xk);
end;


readln;
end.

```

