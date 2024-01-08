- 👋 Hi, I’m @yigithan-kod
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
import pygame
import sys

# Initialize Pygame
pygame.init()

# Constants
WIDTH, HEIGHT = 600, 400
GROUND_HEIGHT = 50
FPS = 30

# Colors
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
RED = (255, 0, 0)

# Bird
bird_width = 40
bird_height = 30
bird_x = WIDTH // 4
bird_y = HEIGHT // 2 - bird_height // 2
bird_velocity = 5

# Pipe
pipe_width = 50
pipe_height = HEIGHT - GROUND_HEIGHT
pipe_x = WIDTH
pipe_gap = 150
pipe_velocity = 5

# Set up the screen
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Flappy Bird")
clock = pygame.time.Clock()

# Fonts
font = pygame.font.SysFont(None, 55)

# Game loop
while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()

        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_SPACE:
                bird_y -= 60

    # Move bird
    bird_y += bird_velocity

    # Move pipe
    pipe_x -= pipe_velocity

    # Check for collisions
    if bird_y > HEIGHT - GROUND_HEIGHT or bird_y < 0:
        pygame.quit()
        sys.exit()

    if pipe_x < 0:
        pipe_x = WIDTH
        pipe_height = HEIGHT - GROUND_HEIGHT - pipe_gap

    if (
        bird_x < pipe_x + pipe_width
        and bird_x + bird_width > pipe_x
        and (bird_y < pipe_height or bird_y + bird_height > pipe_height + pipe_gap)
    ):
        pygame.quit()
        sys.exit()

    # Draw background
    screen.fill(WHITE)

    # Draw bird
    pygame.draw.rect(screen, RED, (bird_x, bird_y, bird_width, bird_height))

    # Draw pipe
    pygame.draw.rect(screen, BLACK, (pipe_x, 0, pipe_width, pipe_height))
    pygame.draw.rect(
        screen,
        BLACK,
        (pipe_x, pipe_height + pipe_gap, pipe_width, HEIGHT - GROUND_HEIGHT - pipe_height - pipe_gap),
    )

    # Draw ground
    pygame.draw.rect(screen, BLACK, (0, HEIGHT - GROUND_HEIGHT, WIDTH, GROUND_HEIGHT))

    # Update the display
    pygame.display.flip()

    # Set the frames per second
    clock.tick(FPS)

<!---
yigithan-kod/yigithan-kod is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
