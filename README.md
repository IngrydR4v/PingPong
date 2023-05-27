# Jogo de Ping Pong 🏓

<img src="pong.gif" align="center"/>

<f2 align = "left"> **O seguinte projeto possui o objetivo de apresentar um jogo de Ping Pong em 2D. Para criar o seu projeto, siga as instruções disponíveis.**</f2>
<hr> </hr>

<f2 align = "left"> **Passo #1**</f2>
<blockquote style="background-color: #F5F8F9;">
    <p> 1.1 Instale a ferramenta PyCharm <p/>
    <p> 1.2 Crie um executável em Python <p/>
    <p> 1.3 Instale o pacote pyInstaller, sendo essa uma ferramenta que permite converter um script Python em um executável independente que pode ser executado em sistemas operacionais Windows, macOS e Linux.<p/>
</blockquote>

<f2 align = "left"> **Passo #2**</f2>
<p> No seu terminal, execute o comando pip install -r requirements.txt. Este comando faz a instalação dos pacotes necessários para que o jogo rode corretamente. <p/>

<f2 align = "left"> **Passo #3**</f2>
<p> Importe os pacotes abaixo:<p/>

    import pygame
    from pygame import mixer
    import sys
    
<blockquote style="background-color: #F5F8F9;">
<p> Linha 1: importa o módulo principal do Pygame, permitindo o acesso a todas as funcionalidades oferecidas pela biblioteca.<p/>
<p> Linha 2: O módulo mixer é responsável pela reprodução de áudio, permitindo que você reproduza músicas e efeitos sonoros nos seus jogos ou aplicativos usando Pygame.<p/>
<p> Linha 3: O módulo sys fornece acesso a algumas variáveis e funções relacionadas ao sistema, como argumentos de linha de comando, interação com o ambiente de execução e finalização do programa.<p/>
</blockquote>

<f2 align = "left"> **Passo #3**</f2>
<p>Utilize funções para inicializar todos os módulos do Pygame e o Mixer.<p/>

    pygame.init()
    mixer.init()
    
<f2 align = "left"> **Passo #4**</f2>
<p>Defina algumas variáveis:<p/>

    SCREEN_WIDTH =800
    SCREEN_HEIGHT = 600
    PADDLE_WIDTH = 10
    PADDLE_HEIGHT = 60
    BALL_SIZE = 10
    PADDLE_SPEED = 4
    BALL_SPEED = 5

    WHITE = (255,255,255)
    BLACK = (0,0,0)

    font_file = "add path"
    font = pygame.font.Font(font_file, 36)
    score_a = 0
    score_b = 0

<f2 align = "left"> **Passo #5**</f2>
<p>Agora vamos carregar e controlar alguns sons do nosso jogo:<p/>

    mixer.music.load("add path")
    mixer.music.set_volume(0.3)
    collision_sound_A = mixer.Sound("add path")
    collision_sound_B = mixer.Sound("add path")
    point_sound = mixer.Sound("add path")
    
<f2 align = "left"> **Passo #6**</f2>
<p>Em seguida identifique o nome da página e permita que o som seja reproduzido:<p/>

    mixer.music.play(-1)
    screen = pygame.display.set_mode((SCREEN_WIDTH,SCREEN_HEIGHT))
    pygame.display.set_caption("PingPong")

<f2 align = "left"> **Passo #7**</f2>
<p>Agora vamos criar objetos e definir as configurações da bola e das raquetes:<p/>

    paddle_a = pygame.Rect(20, SCREEN_HEIGHT // 2 - PADDLE_HEIGHT//2, PADDLE_WIDTH, PADDLE_HEIGHT)
    paddle_b = pygame.Rect(SCREEN_WIDTH - 20 - PADDLE_WIDTH, SCREEN_HEIGHT // 2 - PADDLE_HEIGHT//2, PADDLE_WIDTH, PADDLE_HEIGHT)
    ball =  pygame.Rect(SCREEN_WIDTH //2 - BALL_SIZE // 2, SCREEN_HEIGHT // 2 - BALL_SIZE//2, BALL_SIZE, BALL_SIZE)
    ball_dx, ball_dy = BALL_SPEED, BALL_SPEED
    
<f2 align = "left"> **Passo #8**</f2>
<p>Também é preciso definir algumas configurações sobre o menu do jogo, como feito abaixo:<p/>

    def main_menu():
        while True:
            for event in pygame.event.get():
                if event.type == pygame.QUIT:
                    pygame.quit()
                    sys.exit()

                if event.type == pygame.KEYDOWN:
                    if event.key == pygame.K_SPACE:
                        game_loop()
                    elif event.key == pygame.K_ESCAPE:
                        pygame.quit()
                        sys.exit()

            screen.fill(BLACK)
            title_font = pygame.font.Font(font_file, 36)
            title_text = title_font.render("Pong", True, WHITE)
            title_rect = title_text.get_rect(center=(SCREEN_WIDTH // 2, SCREEN_HEIGHT // 4))

            screen.blit(title_text, title_rect)

            title_font = pygame.font.Font(font_file, 16)
            current_time = pygame.time.get_ticks()

            if current_time % 2000 < 1000:
                title_text1 = title_font.render("Pressione espaço para começar", True, WHITE)
                title_rect1 = title_text1.get_rect(center=(SCREEN_WIDTH // 2, SCREEN_HEIGHT // 4 + 60))
                screen.blit(title_text1, title_rect1)

            pygame.display.flip()
            
<blockquote style="background-color: #F5F8F9;">

<p> 8.1 A função main_menu() é executada em um loop infinito usando "while True". <p/>
<p> 8.2 O loop for event in pygame.event.get(): captura os eventos do Pygame. <p/>
<p> 8.3 Se o evento for do tipo pygame.QUIT, indicando que o usuário fechou a janela do jogo, as funções pygame.quit() e sys.exit() são chamadas para finalizar o Pygame e encerrar o programa. <p/>
<p> 8.4 Se o evento for do tipo pygame.KEYDOWN, verificamos qual tecla foi pressionada. <p/>
<p> 8.5 Se a tecla pressionada for a tecla de espaço (pygame.K_SPACE), a função game_loop() é chamada, provavelmente iniciando o loop principal do jogo. <p/>
<p> 8.6 Se a tecla pressionada for a tecla de escape (pygame.K_ESCAPE) ou se a janela do jogo for fechada, as funções pygame.quit() e sys.exit() são chamadas para encerrar o programa. <p/>
<p> 8.7 O código faz a renderização do menu principal na tela do jogo. <p/>
<p> 8.8 Ele define uma fonte para o título e cria um texto renderizado com o título "Pong".<p/>
<p> 8.9 A posição do texto é definida usando o centro da largura e altura da tela.<p/>
<p> 8.10 O texto é desenhado na tela usando "screen.blit()"<p/>
<p> 8.11 Em seguida, é definida uma fonte menor para a mensagem "Pressione espaço para começar".<p/>
<p> 8.12 O tempo atual é obtido em milissegundos usando "pygame.time.get_ticks()".<p/>
<p> 8.13 Se o tempo atual dividido por 2000 tiver um resto menor que 1000, ou seja, se estiver dentro do intervalo de 0 a 1000 milissegundos, a mensagem "Pressione espaço para começar" é renderizada e desenhada na tela em uma posição específica.<p/>
<p> 8.14 Por fim, "pygame.display.flip()" atualiza a tela com todas as alterações feitas durante o loop.<p/>
</blockquote>
