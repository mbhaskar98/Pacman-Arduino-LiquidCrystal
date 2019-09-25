# Pacman-Arduino-LiquidCrystal
//Displaying Pacman eating the balls row-wise on the lcd screen


// include the library code:
#include <LiquidCrystal.h>

// initialize the library with the numbers of the interface pins
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

// make some custom characters:
byte pac1Def[8] = {
  0b00000,
  0b01110,
  0b11011,
  0b11111,
  0b11111,
  0b01110,
  0b00000,
  0b00000
};
byte pac2Def[8] = {
  0b00000,
  0b01110,
  0b10100,
  0b11000,
  0b11100,
  0b01110,
  0b00000,
  0b00000
};
byte pillDef[8] = {
  0b00000,
  0b00000,
  0b00000,
  0b01100,
  0b01100,
  0b00000,
  0b00000,
  0b00000
};

const byte pac1 = 0x0;
const byte pac2 = 0x1;
const byte pill = 0x2;
const int del = 250;

int x = 0;
int y = 0;
int px = 0;
int py = 0;

void setup() {
  // create a new character
  lcd.createChar(0, pac1Def);
  // create a new character
  lcd.createChar(1, pac2Def);
  // create a new character
  lcd.createChar(2, pillDef);
  // set up the lcd's number of columns and rows: 
  lcd.begin(16, 2);
  // fill the display
  fill();
}

void loop() {
  anim();
  x++;
  if(x>15 && y == 0)
  {
    x = 0;
    y = 1;
  }
  else if(x>15 && y == 1)
  {
    x = 0;
    y = 0;
    fill();
  }
}

// Initial display fill
void fill()
{
  lcd.setCursor(0,0);
  lcd.write(pac1);
  for(int j=0;j<7;j++)
 {
   lcd.write(" ");
   lcd.write(pill);
 }
 lcd.setCursor(0,1);
 lcd.write(pill);
 for(int j=0;j<7;j++)
 {
   lcd.write(" ");
   lcd.write(pill);
 }
}

// character animation
void anim()
{
  
  lcd.setCursor(px,py);
  lcd.write(" ");
  lcd.setCursor(x,y);
  lcd.write(pac1);
  delay(del);
  lcd.setCursor(x,y);
  lcd.write(pac2);
  delay(del);
  px = x;
  py = y;
}
