# hong-final
import turtle
import random

t = turtle.Turtle()
t.speed(0)

red = "#FF0000"
green = "#00FF00"
darkGreen = "#009900"
black = "#000000"
yellow = "#FFFF00"

print('a makes you go left, d makes you go right, w makes you go up, s makes you go down')
print('red apple increases your length, yellow apple decreases your length')

game = [[0 for x in range(10)] for x in range (10)]

def drawSquare(x, y, size, color):
    t.setx(x * 10)
    t.sety(y * 10)

    t.fillcolor(color)

    t.begin_fill()
    for x in range (4):
        t.forward(size)
        t.right(90)
    t.end_fill()

def updateGame(length):
    for y in range (10):
        for x in range (10):
            if game[x][y] > 0:
                game[x][y] += 1
            if game[x][y] > length:
                game[x][y] = 0
                drawSquare(x, y, 10, black)

x = 0
y = 9
time = 0
length = 5
appleX = 0
appleY = 0
dead = False

drawSquare(0, 9, 100, black)

score = 0

while dead == False:
    print("score is", score)
    direction = input('enter direction ')

    if direction == 'w':
        y += 1
    if direction == 'd':
        x += 1
    if direction == 'a':
        x -= 1
    if direction == 's':
        y -= 1
    if direction == 'e':
        dead = True
   
    if (x >= 10):
        dead = True
    if (y >= 10):
        dead = True
    if (x < 0):
        dead = True
    if (y < 0):
        dead = True
   
    if dead == False:

        updateGame(length)

        if game[x][y] == -1:
            length += 1
            score += 1 
            game[x][y] = 0

        if game[x][y] == -2:
            if length >= 2:
                length -= 1
            score += 1
            game[x][y]= 0 
       
        if game[x][y] > 0:
            dead = True
       

        game[x][y] += 1


        drawSquare(x, y, 10, green)

        time += 1

        if time % 10 == 1:
            success = False
            while success == False:
                appleX = (int)(random.random() * 10)
                appleY = (int)(random.random() * 10)
                if (game[appleX][appleY] == 0):
                    game[appleX][appleY] = -1
                    success = True
                    goldOrRed = (int)(random.random()*2)
                    if goldOrRed == 0:
                        drawSquare(appleX, appleY, 10, red)
                        game[appleX][appleY] = -1
                    if goldOrRed == 1:
                        drawSquare(appleX, appleY, 10, yellow)
                        game[appleX][appleY] = -2
