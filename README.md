# Pong-Game
#used in python
import turtle

#Window Setup

wn = turtle.Screen()
wn.title("Pong Game By Ben Nerima")
wn.bgcolor("black")
wn.setup(width=800,height=600)
wn.tracer(0)

#Paddle A

paddle_a = turtle.Turtle()
paddle_a.speed(0)
paddle_a.shape("square")
paddle_a.color("white")
paddle_a.shapesize(stretch_wid = 5, stretch_len=1)
paddle_a.penup()
paddle_a.goto(-350,0)


#paddle B
paddle_b = turtle.Turtle()
paddle_b.speed(0)
paddle_b.shape("square")
paddle_b.color("white")
paddle_b.shapesize(stretch_wid = 5, stretch_len=1)
paddle_b.penup()
paddle_b.goto(350,0)

# Ball
ball = turtle.Turtle()
ball.speed(0)
ball.shape("circle")
ball.color("white")
ball.penup()
ball.goto(0,0)
ball.dx = -1
ball.dy = -1

#pen
pen = turtle.Turtle()
pen.speed(0)
pen.shape("square")
pen.color("white")
pen.penup()
pen.hideturtle()
pen.goto(0,260)
pen.write("Player A: 0 Player B: 0", align= "center", font=("arial", 24, "normal"))

#score

score_1 = 0
score_2 = 0
#Functions
def paddle_a_up():
    y = paddle_a.ycor()
    y = y + 20
    paddle_a.sety(y)

def paddle_a_down():
    y = paddle_a.ycor()
    y = y - 20
    paddle_a.sety(y)

def paddle_b_up():
    y = paddle_b.ycor()
    y = y + 20
    paddle_b.sety(y)

def paddle_b_down():
    y = paddle_b.ycor()
    y = y - 20
    paddle_b.sety(y)

#Keyboard bindings
wn.listen()
wn.onkeypress(paddle_a_up, "w")
wn.onkeypress(paddle_a_down, "s")
wn.onkeypress(paddle_b_up, "Up")
wn.onkeypress(paddle_b_down, "Down")


#main game loop
while True:
    wn.update()

    #Border Checking

    #top and bottom
    if ball.ycor() > 290:
        ball.sety(290)
        ball.dy = ball.dy * -1

    if ball.ycor() < -290:
        ball.sety(-290)
        ball.dy = ball.dy * -1

    #right and left
    if ball.xcor()> 350:
        score_1 = score_1 + 1
        pen.clear()
        #print("Player A: " + str(score_1) + "player B:" str(score_2))
        pen.write("Player A: {} Player B: {}".format(score_1,score_2), align= "center", font=("arial", 24, "normal"))
        ball.goto(0,0)
        ball.dx = ball.dx * -1
           
    if ball.xcor() <-350:
        score_2 = score_2 + 1
        pen.clear()
        pen.write("Player A: {} Player B: {}".format(score_1,score_2), align= "center", font=("arial", 24, "normal"))
        ball.goto(0,0)
        ball.dx = ball.dx * -1

    #move the ball
    ball.setx(ball.xcor()+ ball.dx)
    ball.sety(ball.ycor()+ ball.dy)

    #Paddle And Ball Collision
    if (ball.xcor()< -340 and ball.xcor() > -350) and ball.ycor() < paddle_a.ycor()+ 50 and ball.ycor() > paddle_a.ycor() - 50:
        ball.setx(-340)
        ball.dx = ball.dx * -1
    elif (ball.xcor()> 340 and ball.xcor() > 350) and ball.ycor() < paddle_b.ycor() + 50 and ball.ycor() > paddle_b.ycor() - 50:
        ball.setx(340)
        ball.dx = ball.dx * -1
