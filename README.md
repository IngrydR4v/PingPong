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
<p> 8.5 Se a tecla pressionada for a tecla de espaço (pygame.K_SPACE), a função game_loop() é chamada, provavelmente iniciando o loop pri.ncipal do jogo. <p/>
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

<f2 align = "left"> **Passo #9**</f2>
<p>Em seguida, já podemos começar a programar o jogo, sendo necessário algumas linhas de código:<p/>

    def game_loop():
        global ball_dx, ball_dy, score_a, score_b, ball

        while True:
            for event in pygame.event.get():
                if event.type == pygame.QUIT:
                    pygame.quit()
                    sys.exit()
                if event.type == pygame.KEYDOWN:
                    if event.key == pygame.K_ESCAPE:
                        return
                        
<p>9.1 Nesse trecho, estamos declarando que as variáveis ball_dx, ball_dy, score_a, score_b e ball serão usadas como variáveis globais, criando um loop contínuo que captura eventos como os cliques e ações pelo teclasp e se encerrando apenas após o usuário acessar a tecla "Esc" ou o botão X ☝️.<p/>

            screen.fill(BLACK) 
            pygame.draw.rect(screen, WHITE, paddle_a)
            pygame.draw.rect(screen, WHITE, paddle_b)
            pygame.draw.ellipse(screen, WHITE, ball)
            pygame.draw.aaline(screen, WHITE, (SCREEN_WIDTH // 2, 0), (SCREEN_WIDTH // 2, SCREEN_HEIGHT))
            
<p>9.2 O código acima é responsável por desenhar diferentes formas na tela do jogo utilizando a biblioteca Pygame ☝️.<p/>

            keys = pygame.key.get_pressed()
            
<p>9.3 Utilizada para obter o estado atual de todas as teclas do teclado ☝️.<p/>

            if keys[pygame.K_w] and paddle_a.top > 0:
                paddle_a.y -= PADDLE_SPEED
            if keys[pygame.K_s] and paddle_a.bottom < SCREEN_HEIGHT:
                paddle_a.y += PADDLE_SPEED
                
<p>9.4 Movimento Vertical Raquete 'A' ☝️.<p/>

            if keys[pygame.K_UP] and paddle_b.top > 0:
                paddle_b.y -= PADDLE_SPEED
            if keys[pygame.K_DOWN] and paddle_b.bottom < SCREEN_HEIGHT:
                paddle_b.y += PADDLE_SPEED
                
 <p>9.5 Movimento Vertical Raquete 'B' ☝️.<p/>

            if keys[pygame.K_a] and paddle_a.left > 0:
                paddle_a.x -= PADDLE_SPEED
            if keys[pygame.K_d] and paddle_a.right < SCREEN_WIDTH // 2 - 70:
                paddle_a.x += PADDLE_SPEED
                
<p>9.6 Movimento Horizontal Raquete 'A' ☝️.<p/>

            if keys[pygame.K_UP]:
                self.paddle_b.movey(-self.PADDLE_SPEED)
            if keys[pygame.K_DOWN]:
                self.paddle_b.movey(self.PADDLE_SPEED)
                
<p>9.7 Movimento Vertical Paddle 'B' ☝️.<p/>

            if keys[pygame.K_LEFT] and self.paddle_b.left > self.SCREEN_WIDTH // 2 + 70:
                self.paddle_b.movex(-self.PADDLE_SPEED)
            if keys[pygame.K_RIGHT] and self.paddle_b.right < self.SCREEN_WIDTH:
                self.paddle_b.movex(self.PADDLE_SPEED)
                
<p>9.8 Movimento Horizontal Paddle 'B' ☝️.<p/>

            ball.x += ball_dx
            ball.y += ball_dy

<p>9.9 Atualização da posição da bola ☝️.<p/>

            if ball.colliderect(paddle_a):
                ball.left = paddle_a.right
                ball_dx = -ball_dx
                collision_sound_A.play()

            elif ball.colliderect(paddle_b):
                ball.right = paddle_b.left
                ball_dx = -ball_dx
                collision_sound_B.play()
                
<p>9.10 Verifica se houve colisões com a bola, sendo ajustada à direita ou esquerda de acordo com o local batido, além de configurar a velocidade da bola e os sons que devem ser ouvidos de acordo com o localização da bola ☝️.<p/>

            if self.ball.top <= 0 or self.ball.bottom >= self.SCREEN_HEIGHT:
                self.ball.reverse_dy()
                
<p>9.11 Informa que a bola pode bater tanto em cima quanto em baixo ☝️.<p/>

            if self.ball.left <= 0:
                self.score_b += 1
                self.reset_ball()
                #print(f"Score B: {self.score_b}")
                self.point_sound.play()
                if self.score_b == 10:
                    self.end_game(False)

            elif self.ball.right >= self.SCREEN_WIDTH:
                self.score_a += 1
                self.reset_ball()
                #print(f"Score A: {self.score_a}")
                self.point_sound.play()
                if self.score_a == 10:
                    self.end_game(True)
    
<p>9.12 Mantém a pontuação atualizada ☝️.<p/>

            if ball.top <= 0 or ball.bottom >= SCREEN_HEIGHT:
                ball_dy = -ball_dy
                
<p>9.13 Quando a bola bate na extreminade da tela, é redirecionada para outra localidade ☝️.<p/>

            if ball.left <= 0:
                score_b += 1
                ball.x = SCREEN_WIDTH // 2 - BALL_SIZE // 2
                ball.y = SCREEN_HEIGHT // 2 - BALL_SIZE // 2
                ball_dx = -ball_dx
                point_sound.play()
                # print(score_b)
                if score_b == 10: #Comente
                    end_game(False)
                    
<p>9.14 Informa mais um ponto para o time B ☝️.<p/>

            elif ball.right >= SCREEN_WIDTH:
                score_a += 1
                ball.x = SCREEN_WIDTH // 2 - BALL_SIZE // 2
                ball.y = SCREEN_HEIGHT // 2 - BALL_SIZE // 2
                ball_dx = -ball_dx
                point_sound.play()
                # print(score_a)
                if score_a == 10: #Comente
                    end_game(True)
                    
<p>9.15 Informa mais um ponto para o time A ☝️.<p/>

            score_text = font.render(f"{score_a}  {score_b}", True, WHITE)
            score_rect = score_text.get_rect(center=(SCREEN_WIDTH // 2, 30))
            screen.blit(score_text, score_rect)
            
<p>9.16 Apresenta o placar na tela ☝️.<p/>

            pygame.display.flip()
            
<p>9.17 Mantém a tela atualizada ☝️.<p/>

            clock = pygame.time.Clock()
            clock.tick(60)
            
<p>9.18 Controla o tempo da partida ☝️.<p/>

<f2 align = "left"> **Passo #10**</f2>
<p>Assim já podemos nos encaminhar para a reta final do jogo... Olha só:<p/>

        def end_game(winner): 
            while True:
                for event in pygame.event.get():
                    if event.type == pygame.QUIT:
                        pygame.quit()
                        sys.exit()
                    if event.type == pygame.KEYDOWN:
                        if event.key == pygame.K_SPACE:
                            reset_game()
                            return
                        elif event.key == pygame.K_ESCAPE:
                            pygame.quit()
                            sys.exit()


                mixer.music.stop()
                screen.fill(BLACK)
                if winner:
                    winner_text = "Player 2 Wins!"
                else:
                    winner_text = "Player 1 Wins!"

                winner_font = pygame.font.Font(font_file, 36)
                winner_render = winner_font.render(winner_text, True, WHITE)
                winner_rect = winner_render.get_rect(center=(SCREEN_WIDTH // 2, SCREEN_HEIGHT // 4))
                screen.blit(winner_render, winner_rect)
                pygame.display.flip()

<p>A função acima lida com o fim do jogo, exibindo o vencedor na tela e permitindo que o jogador reinicie o jogo ou encerre o programa.<p/>
<blockquote style="background-color: #F5F8F9;">
<p> 10.1 O código entra em um loop while True para aguardar ações do usuário.<p/>

<p> 10. 2 Ele captura os eventos do Pygame usando pygame.event.get() e itera sobre eles.<p/>

<p> 10.3 Se o evento capturado for do tipo pygame.QUIT (o usuário clicou no botão "X" para fechar a janela), o programa é encerrado chamando pygame.quit() e sys.exit().<p/>

<p>10.4 Se o evento capturado for do tipo pygame.KEYDOWN (o usuário pressionou uma tecla), são realizadas as seguintes verificações:
-- Se a tecla pressionada for a tecla "SPACE", o jogo é reiniciado chamando a função reset_game() (não mostrada no código) e a função end_game é encerrada com o comando return.
-- Se a tecla pressionada for a tecla "ESCAPE", o programa é encerrado chamando pygame.quit() e sys.exit().<p/>
    
<p>10.5 Em seguida, a música de fundo é interrompida (mixer.music.stop()), a tela é preenchida com a cor preta (screen.fill(BLACK)), e um texto é renderizado na tela dependendo do vencedor do jogo.<p/>

<p> 10.6 O texto é renderizado usando uma fonte definida anteriormente e a cor branca (winner_font.render(winner_text, True, WHITE)).<p/>

<p> 10.7 A posição do texto é calculada e colocado no centro da tela (winner_rect = winner_render.get_rect(center=(SCREEN_WIDTH // 2, SCREEN_HEIGHT // 4))).<p/>

<p> 10.8 O texto é exibido na tela usando screen.blit(winner_render, winner_rect). <p/>

<p>10.9 Por fim, as mudanças são atualizadas na tela com pygame.display.flip().<p/> 
</blockquote>
