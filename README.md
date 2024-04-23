import pygame
import random

# Khởi tạo Pygame
pygame.init()

# Các biến cấu hình
SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)

# Các biến trạng thái
game_over = False

# Khởi tạo cửa sổ trò chơi
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("Chopping Wood Adventure")

# Load hình ảnh
player_img = pygame.image.load('player.png')
tree_img = pygame.image.load('tree.png')
god_img = pygame.image.load('god.png')

# Khởi tạo vị trí ban đầu
player_x = 50
player_y = SCREEN_HEIGHT - player_img.get_height() - 50
tree_x = SCREEN_WIDTH - tree_img.get_width() - 50
tree_y = SCREEN_HEIGHT - tree_img.get_height() - 50
god_x = SCREEN_WIDTH // 2 - god_img.get_width() // 2
god_y = 50

# Khởi tạo điểm số
score = 0

# Hàm vẽ đối tượng
def draw_objects():
    screen.blit(player_img, (player_x, player_y))
    screen.blit(tree_img, (tree_x, tree_y))
    screen.blit(god_img, (god_x, god_y))

# Vòng lặp chính
clock = pygame.time.Clock()
while not game_over:
    screen.fill(WHITE)
    
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            game_over = True
        elif event.type == pygame.KEYDOWN:
            if event.key == pygame.K_SPACE:
                # Kiểm tra va chạm giữa cậu bé và cây
                if player_x + player_img.get_width() >= tree_x and player_y + player_img.get_height() >= tree_y:
                    score += 1
                    # Di chuyển cây và thần ngẫu nhiên
                    tree_x = random.randint(50, SCREEN_WIDTH - tree_img.get_width() - 50)
                    tree_y = SCREEN_HEIGHT - tree_img.get_height() - 50
                    god_x = random.randint(50, SCREEN_WIDTH - god_img.get_width() - 50)
    
    # Di chuyển cậu bé
    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT]:
        player_x -= 5
    if keys[pygame.K_RIGHT]:
        player_x += 5
    
    # Vẽ các đối tượng
    draw_objects()
    
    # Hiển thị điểm số
    font = pygame.font.SysFont(None, 36)
    text = font.render("Score: " + str(score), True, BLACK)
    screen.blit(text, (10, 10))
    
    # Cập nhật cửa sổ
    pygame.display.flip()
    
    # Đặt tốc độ khung hình
    clock.tick(60)


<!---
coderplaygame/coderplaygame is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
