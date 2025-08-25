.. include:: common.txtimport pygame from pygame.locals import *

--- настройки ---

TILE_SIZE = 32 WIDTH, HEIGHT = 800, 600 ROWS, COLS = HEIGHT // TILE_SIZE, WIDTH // TILE_SIZE

цвета

DIRT = (155, 118, 83) GRASS = (106, 190, 48) SKY = (135, 206, 235)

--- инициализация ---

pygame.init() screen = pygame.display.set_mode((WIDTH, HEIGHT)) clock = pygame.time.Clock()

--- карта мира ---

world = [[0 for _ in range(COLS)] for _ in range(ROWS)] for r in range(ROWS): for c in range(COLS): if r > ROWS // 2: world[r][c] = 1  # земля if r == ROWS // 2: world[r][c] = 2  # трава

--- игрок ---

player_x, player_y = WIDTH//2, HEIGHT//2 player_speed = 5

--- функции ---

def draw_world(): for r in range(ROWS): for c in range(COLS): block = world[r][c] if block == 1: color = DIRT elif block == 2: color = GRASS else: continue pygame.draw.rect(screen, color, (cTILE_SIZE, rTILE_SIZE, TILE_SIZE, TILE_SIZE))

--- цикл игры ---

running = True while running: screen.fill(SKY)

for event in pygame.event.get():
    if event.type == QUIT:
        running = False
    if event.type == MOUSEBUTTONDOWN:
        mx, my = pygame.mouse.get_pos()
        c, r = mx // TILE_SIZE, my // TILE_SIZE
        if event.button == 1:  # ЛКМ - ломать
            world[r][c] = 0
        if event.button == 3:  # ПКМ - ставить
            world[r][c] = 1

keys = pygame.key.get_pressed()
if keys[K_LEFT]:
    player_x -= player_speed
if keys[K_RIGHT]:
    player_x += player_speed
if keys[K_UP]:
    player_y -= player_speed
if keys[K_DOWN]:
    player_y += player_speed

draw_world()
pygame.draw.rect(screen, (255,0,0), (player_x, player_y, TILE_SIZE, TILE_SIZE))

pygame.display.flip()
clock.tick(60)

pygame.quit()



:mod:`pygame.locals`
====================

.. module:: pygame.locals
   :synopsis: pygame constants

| :sl:`pygame constants`

This module contains various constants used by pygame. Its contents are
automatically placed in the pygame module namespace. However, an application
can use ``pygame.locals`` to include only the pygame constants with a ``from
pygame.locals import *``.

Detailed descriptions of the various constants can be found throughout the
pygame documentation. Here are the locations of some of them.

   - The :mod:`pygame.display` module contains flags like ``FULLSCREEN`` used
     by :func:`pygame.display.set_mode`.
   - The :mod:`pygame.event` module contains the various event types.
   - The :mod:`pygame.key` module lists the keyboard constants and modifiers
     (``K_``\* and ``MOD_``\*) relating to the ``key`` and ``mod`` attributes of
     the ``KEYDOWN`` and ``KEYUP`` events.
   - The :mod:`pygame.time` module defines ``TIMER_RESOLUTION``.

.. ## pygame.locals ##
