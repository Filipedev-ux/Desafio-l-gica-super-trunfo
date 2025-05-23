# Desafio-l-gica-super-trunfo
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h> // Para gerar números aleatórios

// Define a estrutura para uma carta do Super Trunfo
typedef struct {
    char nome[50];
    int ataque;
    int defesa;
    int magia;
} Carta;

// Função para exibir uma carta
void exibirCarta(Carta carta) {
    printf("Nome: %s\n", carta.nome);
    printf("Ataque: %d\n", carta.ataque);
    printf("Defesa: %d\n", carta.defesa);
    printf("Magia: %d\n", carta.magia);
    printf("--------------------\n");
}

// Função para comparar cartas baseado no atributo escolhido
// Retorna 1 se o jogador 1 vence, 2 se o jogador 2 vence, 0 se empate
int compararCartas(Carta cartaJogador1, Carta cartaJogador2, int atributo) {
    switch (atributo) {
        case 1: // Ataque
            if (cartaJogador1.ataque > cartaJogador2.ataque) return 1;
            if (cartaJogador2.ataque > cartaJogador1.ataque) return 2;
            break;
        case 2: // Defesa
            if (cartaJogador1.defesa > cartaJogador2.defesa) return 1;
            if (cartaJogador2.defesa > cartaJogador1.defesa) return 2;
            break;
        case 3: // Magia
            if (cartaJogador1.magia > cartaJogador2.magia) return 1;
            if (cartaJogador2.magia > cartaJogador1.magia) return 2;
            break;
        default:
            printf("Atributo inválido!\n");
            return 0; // Em caso de erro, considera empate
    }
    return 0; // Empate
}

int main() {
    // Inicializa o gerador de números aleatórios
    srand(time(NULL));

    // Cria algumas cartas de exemplo (um baralho pequeno)
    Carta baralho[5];
    strcpy(baralho[0].nome, "Dragao Vermelho");
    baralho[0].ataque = 90;
    baralho[0].defesa = 70;
    baralho[0].magia = 60;

    strcpy(baralho[1].nome, "Elfo Arqueiro");
    baralho[1].ataque = 75;
    baralho[1].defesa = 60;
    baralho[1].magia = 80;

    strcpy(baralho[2].nome, "Guerreiro Anao");
    baralho[2].ataque = 80;
    baralho[2].defesa = 95;
    baralho[2].magia = 40;

    strcpy(baralho[3].nome, "Mago Supremo");
    baralho[3].ataque = 60;
    baralho[3].defesa = 50;
    baralho[3].magia = 98;

    strcpy(baralho[4].nome, "Goblin Ladrao");
    baralho[4].ataque = 65;
    baralho[4].defesa = 40;
    baralho[4].magia = 30;

    int numCartasBaralho = sizeof(baralho) / sizeof(baralho[0]);

    // Simula a distribuição de cartas para dois jogadores (simplificado)
    // Para este exemplo, cada jogador recebe uma carta aleatória por rodada
    // Um jogo real teria distribuição e gerenciamento de montes de cartas

    Carta cartaJogador1;
    Carta cartaJogador2;

    int pontuacaoJogador1 = 0;
    int pontuacaoJogador2 = 0;
    int atributoEscolhido;
    int vencedorRodada;

    printf("--- SUPER TRUNFO INICIANTE ---\n\n");

    // Loop principal do jogo (ex: 3 rodadas)
    for (int rodada = 1; rodada <= 3; rodada++) {
        printf("\n--- Rodada %d ---\n", rodada);

        // Jogador 1 recebe uma carta aleatória
        cartaJogador1 = baralho[rand() % numCartasBaralho];
        printf("Jogador 1, sua carta:\n");
        exibirCarta(cartaJogador1);

        // Jogador 2 recebe uma carta aleatória (diferente da do jogador 1, idealmente)
        // Simplificacao: pode pegar a mesma, mas em um jogo real seria diferente.
        cartaJogador2 = baralho[rand() % numCartasBaralho];
        // Nao mostraremos a carta do Jogador 2 ainda para o Jogador 1 escolher o atributo

        printf("Jogador 1, escolha o atributo para comparar:\n");
        printf("1. Ataque\n");
        printf("2. Defesa\n");
        printf("3. Magia\n");
        printf("Sua escolha: ");
        scanf("%d", &atributoEscolhido);

        printf("\nCarta do Jogador 2:\n");
        exibirCarta(cartaJogador2);

        vencedorRodada = compararCartas(cartaJogador1, cartaJogador2, atributoEscolhido);

        if (vencedorRodada == 1) {
            printf("Jogador 1 venceu a rodada!\n");
            pontuacaoJogador1++;
        } else if (vencedorRodada == 2) {
            printf("Jogador 2 venceu a rodada!\n");
            pontuacaoJogador2++;
        } else {
            printf("Empate na rodada!\n");
        }

        printf("Placar: Jogador 1 [%d] x [%d] Jogador 2\n", pontuacaoJogador1, pontuacaoJogador2);
        printf("Pressione Enter para a proxima rodada...");
        // Limpa o buffer de entrada antes de getchar()
        while (getchar() != '\n'); // Consome o '\n' deixado pelo scanf
        getchar(); // Espera o Enter
    }

    printf("\n--- FIM DE JOGO ---\n");
    printf("Placar Final: Jogador 1 [%d] x [%d] Jogador 2\n", pontuacaoJogador1, pontuacaoJogador2);

    if (pontuacaoJogador1 > pontuacaoJogador2) {
        printf("Jogador 1 eh o grande campeao!\n");
    } else if (pontuacaoJogador2 > pontuacaoJogador1) {
        printf("Jogador 2 eh o grande campeao!\n");
    } else {
        printf("O jogo terminou em empate!\n");
    }

    return 0;
}
