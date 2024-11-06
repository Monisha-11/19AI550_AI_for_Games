# Ex.No: 10  Mini Project 
#### DATE: 08/10/2024                                                                          
#### REGISTER NUMBER : 212221240029

### AIM: 

The aim of this program is to create a simple Pong game using Pygame, where the user controls the left paddle and the AI controls the right paddle. The goal is to hit the ball back and forth without letting it touch the edge of the screen.

### Algorithm:

#### Initialization

1. Initialize Pygame and set up the game window with a width and height of 640x480 pixels.
2. Set up the title of the window to "Pong Game".
3. Initialize the paddles, ball, and score variables.

#### Game Loop

1. Handle events:
   + Check for the QUIT event to exit the game.
   + Check for keyboard input to move the left paddle.
2. Move the paddles:
   + Move the left paddle based on user input.
   + Move the right paddle based on the AI's strategy (see below).
3. Move the ball:
   + Update the ball's position based on its speed and direction.
   + Check for collisions with the walls and paddles.
   + Bounce the ball off the walls and paddles if necessary.
4. Check for goals:
   + If the ball touches the left or right edge of the screen, increment the score accordingly.
   + Reset the ball's position to the center of the screen.
5. Draw everything:
   + Clear the screen.
   + Draw the paddles, ball, and score.

#### AI Strategy

1. If the ball is on the right side of the screen, move the right paddle towards the ball's y-coordinate.
2. If the ball is moving towards the right paddle, move the paddle towards the ball's y-coordinate.
3. If the ball is moving away from the right paddle, move the paddle towards the center of the screen.

### Program:
```python
import pygame
import random

# Initialize Pygame
pygame.init()

# Set up the game window
screen_width = 640
screen_height = 480
screen = pygame.display.set_mode((screen_width, screen_height))

# Set up the title of the window
pygame.display.set_caption("Pong Game")

# Set up the paddles
paddle_width = 10
paddle_height = 100
paddle_speed = 5

paddle1_x = 10
paddle1_y = screen_height / 2 - paddle_height / 2

paddle2_x = screen_width - 20
paddle2_y = screen_height / 2 - paddle_height / 2

# Set up the ball
ball_size = 10
ball_speed = 5

ball_x = screen_width / 2
ball_y = screen_height / 2
ball_dx = random.choice([-1, 1])
ball_dy = random.choice([-1, 1])

# Set up the score
score1 = 0
score2 = 0

# Set up the AI
ai_difficulty = 0.5

# Game loop
while True:
    # Handle events
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()

    # Move the paddles
    keys = pygame.key.get_pressed()
    if keys[pygame.K_UP]:
        paddle1_y -= paddle_speed
    if keys[pygame.K_DOWN]:
        paddle1_y += paddle_speed

    # AI moves the second paddle
    if ball_x > screen_width / 2:
        if ball_y < paddle2_y + paddle_height / 2:
            paddle2_y -= paddle_speed
        elif ball_y > paddle2_y + paddle_height / 2:
            paddle2_y += paddle_speed

    # Move the ball
    ball_x += ball_dx * ball_speed
    ball_y += ball_dy * ball_speed

    # Bounce the ball off the walls
    if ball_y < 0 or ball_y > screen_height - ball_size:
        ball_dy *= -1

    # Check for collisions with the paddles
    if ball_x < paddle1_x + paddle_width and ball_y > paddle1_y and ball_y < paddle1_y + paddle_height:
        ball_dx *= -1
    elif ball_x > paddle2_x - paddle_width and ball_y > paddle2_y and ball_y < paddle2_y + paddle_height:
        ball_dx *= -1

    # Check for goals
    if ball_x < 0:
        score2 += 1
        ball_x = screen_width / 2
        ball_y = screen_height / 2
        ball_dx = random.choice([-1, 1])
        ball_dy = random.choice([-1, 1])
    elif ball_x > screen_width - ball_size:
        score1 += 1
        ball_x = screen_width / 2
        ball_y = screen_height / 2
        ball_dx = random.choice([-1, 1])
        ball_dy = random.choice([-1, 1])

    # Draw everything
    screen.fill((0, 0, 0))
    pygame.draw.rect(screen, (255, 255, 255), (paddle1_x, paddle1_y, paddle_width, paddle_height))
    pygame.draw.rect(screen, (255, 255, 255), (paddle2_x, paddle2_y, paddle_width, paddle_height))
    pygame.draw.ellipse(screen, (255, 255, 255), (ball_x, ball_y, ball_size, ball_size))
    pygame.draw.aaline(screen, (255, 255, 255), (screen_width / 2, 0), (screen_width / 2, screen_height))
    font = pygame.font.Font(None, 36)
    text = font.render(f"{score1} - {score2}", True, (255, 255, 255))
    screen.blit(text, (screen_width / 2 - 20, 20))

    # Update the screen
    pygame.display.flip()
    pygame.time.Clock().tick(60)

```

### Output:

<img width="476" alt="image" src="https://github.com/user-attachments/assets/88486ecd-3e1a-4b64-9122-95dcb9b2a3c6">


### Result:
The program creates a simple Pong game where a user controls the left paddle and an AI controls the right paddle, with the goal of hitting the ball back and forth without letting it touch the edge of the screen.
