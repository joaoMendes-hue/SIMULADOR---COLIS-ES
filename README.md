import pygame
import random
import math

# -------------------------
# Configurações
# -------------------------
WIDTH = 800
HEIGHT = 600

N_BOLAS = 15
RAIO = 15

FPS = 60

# -------------------------
# Classe Bola
# -------------------------
class Bola:

    def __init__(self):
        self.x = random.randint(RAIO, WIDTH - RAIO)
        self.y = random.randint(RAIO, HEIGHT - RAIO)

        self.vx = random.uniform(-150, 150)
        self.vy = random.uniform(-150, 150)

        self.raio = RAIO

        self.cor = (
            random.randint(50,255),
            random.randint(50,255),
            random.randint(50,255)
        )

    def mover(self, dt):

        self.x += self.vx * dt
        self.y += self.vy * dt

        # paredes verticais
        if self.x - self.raio <= 0:
            self.x = self.raio
            self.vx *= -1

        if self.x + self.raio >= WIDTH:
            self.x = WIDTH - self.raio
            self.vx *= -1

        # paredes horizontais
        if self.y - self.raio <= 0:
            self.y = self.raio
            self.vy *= -1

        if self.y + self.raio >= HEIGHT:
            self.y = HEIGHT - self.raio
            self.vy *= -1

    def desenhar(self, tela):
        pygame.draw.circle(
            tela,
            self.cor,
            (int(self.x), int(self.y)),
            self.raio
        )

# -------------------------
# Colisão entre bolas
# -------------------------
def colisao(b1, b2):

    dx = b2.x - b1.x
    dy = b2.y - b1.y

    dist = math.sqrt(dx*dx + dy*dy)

    if dist == 0:
        return

    if dist < b1.raio + b2.raio:

        nx = dx / dist
        ny = dy / dist

        dvx = b1.vx - b2.vx
        dvy = b1.vy - b2.vy

        vel_rel = dvx*nx + dvy*ny

        if vel_rel > 0:
            return

        impulso = -2 * vel_rel / 2

        b1.vx += impulso * nx
        b1.vy += impulso * ny

        b2.vx -= impulso * nx
        b2.vy -= impulso * ny

        # separa as bolas para evitar sobreposição
        overlap = (b1.raio + b2.raio) - dist

        b1.x -= overlap * nx / 2
        b1.y -= overlap * ny / 2

        b2.x += overlap * nx / 2
        b2.y += overlap * ny / 2

# -------------------------
# Programa principal
# -------------------------
pygame.init()

screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Simulação de Colisões")

clock = pygame.time.Clock()

bolas = [Bola() for _ in range(N_BOLAS)]

running = True

while running:

    dt = clock.tick(FPS) / 1000.0

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    for bola in bolas:
        bola.mover(dt)

    for i in range(N_BOLAS):
        for j in range(i + 1, N_BOLAS):
            colisao(bolas[i], bolas[j])

    screen.fill((20,20,20))

    for bola in bolas:
        bola.desenhar(screen)

    pygame.display.flip()

pygame.quit()
