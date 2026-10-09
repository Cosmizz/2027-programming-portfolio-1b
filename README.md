# # OOP Calculator for Programming 1

![Calculator](https://github.com/Cosmizz/2027-programming-portfolio-1b/blob/main/images/Calc01.png?raw=true)
[Link to source code](//Ian Gorchos | 15 sept 2026 | Calculator

Button[] numButtons = new Button[11];
Button[] opButtons = new Button[7];
float l, r, result;
char op;
boolean left, newEntry;
String displayVal;

void setup() {
  size(150, 230);
  resetCalc();


  numButtons[0] = new Button(30, 190, 60, 30, '0');
  numButtons[1] = new Button(83, 190, 40, 30, '.');
  numButtons[2] = new Button(20, 160, 20, 20, '1');
  numButtons[3] = new Button(50, 160, 20, 20, '2');
  numButtons[4] = new Button(80, 160, 20, 20, '3');
  numButtons[5] = new Button(20, 130, 20, 20, '4');
  numButtons[6] = new Button(50, 130, 20, 20, '5');
  numButtons[7] = new Button(80, 130, 20, 20, '6');
  numButtons[8] = new Button(20, 100, 20, 20, '7');
  numButtons[9] = new Button(50, 100, 20, 20, '8');
  numButtons[10] = new Button(80, 100, 20, 20, '9');

  // Operator buttons
  opButtons[0] = new Button(125, 160, 40, 90, '=');
  opButtons[1] = new Button(20, 75, 20, 20, 'C');
  opButtons[2] = new Button(50, 75, 20, 20, '/');
  opButtons[3] = new Button(80, 75, 20, 20, 'X');
  opButtons[4] = new Button(125, 75, 20, 20, '-');
  opButtons[5] = new Button(125, 100, 20, 20, '+');
  opButtons[6] = new Button(180, 75, 20, 20, '%');
}

void draw() {
  background(33);
  drawDisplay();
  
  for (int i = 0; i < numButtons.length; i++) {
    numButtons[i].display();
    numButtons[i].mouseOver(mouseX, mouseY);
  }

  for (int i = 0; i < opButtons.length; i++) {
    opButtons[i].display();
    opButtons[i].mouseOver(mouseX, mouseY);
  }
}

void drawDisplay() {
  rectMode(CENTER);
  fill(220);
  rect(width / 2, 25, 110, 40);
  fill(0);
  textAlign(RIGHT, CENTER);
  textSize(16);
  text(displayVal, width - 30, 25);
}

void mouseReleased() {
  // Check number buttons
  for (int i = 0; i < numButtons.length; i++) {
    if (numButtons[i].hover) {
      handleEvent(numButtons[i].val, true);
    }
  }

  // Check operator buttons
  for (int i = 0; i < opButtons.length; i++) {
    if (opButtons[i].hover) {
      handleEvent(opButtons[i].val, false);
    }
  }
}

void handleEvent(char val, boolean isNum) {
  if (isNum) {
    if (val == '.') {
      if (newEntry || displayVal.equals("0.0")) {
        displayVal = "0.";
        newEntry = false;
      } else if (!displayVal.contains(".")) {
        displayVal += ".";
      }
    } else {
      if (newEntry || displayVal.equals("0.0")) {
        displayVal = str(val);
        newEntry = false;
      } else {
        displayVal += val;
      }
    }

    if (left) {
      l = float(displayVal);
    } else {
      r = float(displayVal);
    }
  } else {
    // Handle Operators
    if (val == 'C') {
      resetCalc();
    } else if (val == '=') {
      preformCalc();
    } else if (val == '+' || val == '-' || val == 'X' || val == '/' || val == '%') {
      op = val;
      left = false;
      newEntry = true;
    } else if (val == 's') {
      if (left) {
        l = sqrt(l);
        displayVal = str(l);
      } else {
        r = sqrt(r);
        displayVal = str(r);
      }
    }
  }
}

void preformCalc() {
  if (op == '+') {
    result = l + r;
  } else if (op == '-') {
    result = l - r;
  } else if (op == '/') {
    result = (r != 0) ? l / r : 0.0; // Avoid division by zero
  } else if (op == 'X') {
    result = l * r;
  } else if (op == '%') {
    result = l % r;
  } else {
    result = l;
  }

  displayVal = str(result);
  l = result;    
  left = true;   
  newEntry = true;
}

void resetCalc() {
  l = 0.0;
  r = 0.0;
  result = 0.0;
  op = ' ';
  displayVal = "0.0";
  left = true;
  newEntry = true;
}

void keyPressed() {
  // Numbers (Top Row: 48-57, Numpad: 96-105)
  if ((keyCode >= 48 && keyCode <= 57)) {
    handleEvent((char) key, true);
  } else if (keyCode >= 96 && keyCode <= 105) {
    handleEvent((char) ('0' + (keyCode - 96)), true);
  } else if (key == '.') {
    handleEvent('.', true);
  } 
  // Operators
  else if (key == '+' || key == '-' || key == '/' || key == '%') {
    handleEvent(key, false);
  } else if (key == '*' || key == 'x' || key == 'X') {
    handleEvent('X', false);
  } else if (key == '=' || keyCode == ENTER || keyCode == RETURN) {
    handleEvent('=', false);
  } else if (key == 'c' || key == 'C' || keyCode == BACKSPACE) {
    handleEvent('C', false);
  }
})

## Overview
[Write 2–3 sentences explaining what you are building
and what a user can do with it.]

## Current Status
Working:
- [A feature you have tested]
- [Another feature you have tested]

Still in progress:
- [A requirement you are finishing]

## How to Run
Built with Processing.
Processing version: [Your version]

[After the project files are uploaded, identify the
project folder and main .pde file to open and run.]

## Controls
Mouse:
[Explain how to use the buttons.]

Keyboard:
[List keys that currently work and what they do.
Identify planned controls as not yet implemented.]

## Project Files
[Identify the main sketch and other tabs or assets
you will upload.]

## Testing
[Record one test: actions, expected result,
and actual result.]

## Next Step
[Name the specific behavior you will build or fix next.]
