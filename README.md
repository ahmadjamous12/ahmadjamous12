import pygame
import random

# إعدادات اللعبة
WIDTH, HEIGHT = 800, 600
FPS = 60

# ألوان
WHITE = (255, 255, 255)
RED = (255, 0, 0)
BLUE = (0, 0, 255)

# الفئات
class Player:
    def __init__(self, x, y):
        self.rect = pygame.Rect(x, y, 50, 50)
        self.health = 100

    def move(self, dx, dy):
        self.rect.x += dx
        self.rect.y += dy

    def draw(self, surface):
        pygame.draw.rect(surface, BLUE, self.rect)

class Enemy:
    def __init__(self, x, y):
        self.rect = pygame.Rect(x, y, 50, 50)
        self.health = 100

    def attack(self, damage):
        self.health -= damage

    def draw(self, surface):
        pygame.draw.rect(surface, RED, self.rect)

# تهيئة Pygame
pygame.init()
screen = pygame.display.set_mode((WIDTH, HEIGHT))
clock = pygame.time.Clock()

# إنشاء اللاعب والعدو
player = Player(100, 100)
enemy = Enemy(500, 100)

running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT]:
        player.move(-5, 0)
    if keys[pygame.K_RIGHT]:
        player.move(5, 0)
    if keys[pygame.K_UP]:
        player.move(0, -5)
    if keys[pygame.K_DOWN]:
        player.move(0, 5)
    if keys[pygame.K_SPACE]:  # زر الهجوم
        enemy.attack(20)

    # تحديث الشاشة
    screen.fill(WHITE)
    player.draw(screen)
    enemy.draw(screen)

    pygame.display.flip()
    clock.tick(FPS)

pygame.quit()
