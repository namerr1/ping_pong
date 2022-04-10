# ping_pong
первая версия
from pygame import *

class Game(sprite.Sprite):
    def __init__(self, player_image, player_x, player_y, player_speed, a = 100):
        super().__init__()
        self.a = a
        self.image = transform.scale(image.load(player_image), (self.a, self.a))
        self.speed = player_speed
        self.rect = self.image.get_rect()
        self.rect.x = player_x
        self.rect.y = player_y

    def reset(self):
        window.blit(self.image, (self.rect.x, self.rect.y))

class Player(Game):

    def update_1(self):
        
        key_pressed = key.get_pressed()
        if key_pressed[K_LEFT] and self.rect.x > 10:
            self.rect.y -= self.speed
        if key_pressed[K_RIGHT] and self.rect.x < 580:
            self.rect.y += self.speed

    def update_2(self):
        key_pressed = key.get_pressed()
        if key_pressed[K_UP] and self.rect.y > 10:
            self.rect.y -= self.speed
        if key_pressed[K_DOWN] and self.rect.y < 580:
            self.rect.y += self.speed


class Enemy(Game):
    
    def dviz(self):
        if self.rect.y > 480:
            self.rect.y = 0
            self.rect.x = randint(0, 600)

        else:
            self.rect.y += self.speed


window = display.set_mode((700, 500))
display.set_caption('Игра Пинг-понг')
fon = transform.scale(image.load('BB172NY4.jpg'), (700, 500))
rocket1 = Player('rocket.png', 100, 100, 20, 200)
rocket2 = Player('rocket.png', 500, 300, 20, 200)
ball = Enemy('one.png', 200, 200, 30)
clock = time.Clock()
FPS = 60
t = True

while t:
    k = event.get()
    window.blit(fon, (0, 0))
    rocket1.reset()
    rocket1.update_1()
    rocket2.reset()
    rocket2.update_2()
    ball.reset()

    for m in k:
        if m.type == QUIT:
            t = False


    display.update()
    clock.tick(FPS)


