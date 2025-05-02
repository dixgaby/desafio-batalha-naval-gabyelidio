#include <stdio.h>

#define TAM_TABULEIRO 10 // Tamanho do tabuleiro (10x10)
#define TAM_NAVIO 3      // Tamanho fixo dos navios
#define TAM_HABILIDADE 5 // Tamanho das matrizes de habilidades (5x5)

void aplicarHabilidade(int tabuleiro[TAM_TABULEIRO][TAM_TABULEIRO], int habilidade[TAM_HABILIDADE][TAM_HABILIDADE], int origemLinha, int origemColuna) {
    for (int i = 0; i < TAM_HABILIDADE; i++) {
        for (int j = 0; j < TAM_HABILIDADE; j++) {
            // Verifica se a célula da habilidade afeta alguma posição (valor 1)
            if (habilidade[i][j] == 1) {
                // Calcula a posição no tabuleiro e valida se está dentro dos limites
                int linha = origemLinha + i - TAM_HABILIDADE / 2;
                int coluna = origemColuna + j - TAM_HABILIDADE / 2;
                if (linha >= 0 && linha < TAM_TABULEIRO && coluna >= 0 && coluna < TAM_TABULEIRO) {
                    if (tabuleiro[linha][coluna] != 3) { // Não sobrepõe navios
                        tabuleiro[linha][coluna] = 5; // Marca área afetada
                    }
                }
            }
        }
    }
}

int main() {
    // Declaração do tabuleiro (matriz 10x10) e inicialização com água (valor 0)
    int tabuleiro[TAM_TABULEIRO][TAM_TABULEIRO] = {0};

    // Coordenadas iniciais dos navios
    int linhaNavioVertical = 2, colunaNavioVertical = 5; 
    int linhaNavioHorizontal = 6, colunaNavioHorizontal = 3; 
    int linhaNavioDiagonal1 = 0, colunaNavioDiagonal1 = 0; 
    int linhaNavioDiagonal2 = 8, colunaNavioDiagonal2 = 9;

    // Posiciona navios no tabuleiro
    for (int i = 0; i < TAM_NAVIO; i++) {
        tabuleiro[linhaNavioVertical + i][colunaNavioVertical] = 3;
        tabuleiro[linhaNavioHorizontal][colunaNavioHorizontal + i] = 3;
        tabuleiro[linhaNavioDiagonal1 + i][colunaNavioDiagonal1 + i] = 3;
        tabuleiro[linhaNavioDiagonal2 - i][colunaNavioDiagonal2 - i] = 3;
    }

    // Matrizes de habilidades especiais (Cone, Cruz, Octaedro)
    int habilidadeCone[TAM_HABILIDADE][TAM_HABILIDADE] = {
        {0, 0, 1, 0, 0},
        {0, 1, 1, 1, 0},
        {1, 1, 1, 1, 1},
        {0, 0, 0, 0, 0},
        {0, 0, 0, 0, 0}
    };

    int habilidadeCruz[TAM_HABILIDADE][TAM_HABILIDADE] = {
        {0, 0, 1, 0, 0},
        {0, 0, 1, 0, 0},
        {1, 1, 1, 1, 1},
        {0, 0, 1, 0, 0},
        {0, 0, 1, 0, 0}
    };

    int habilidadeOctaedro[TAM_HABILIDADE][TAM_HABILIDADE] = {
        {0, 0, 1, 0, 0},
        {0, 1, 1, 1, 0},
        {1, 1, 1, 1, 1},
        {0, 1, 1, 1, 0},
        {0, 0, 1, 0, 0}
    };

    // Aplica habilidades no tabuleiro
    aplicarHabilidade(tabuleiro, habilidadeCone, 4, 4); // Exemplo: Cone em (4, 4)
    aplicarHabilidade(tabuleiro, habilidadeCruz, 7, 7); // Exemplo: Cruz em (7, 7)
    aplicarHabilidade(tabuleiro, habilidadeOctaedro, 2, 2); // Exemplo: Octaedro em (2, 2)

    // Exibição do tabuleiro completo
    printf("Tabuleiro:\n");
    for (int i = 0; i < TAM_TABULEIRO; i++) {
        for (int j = 0; j < TAM_TABULEIRO; j++) {
            printf("%d ", tabuleiro[i][j]);
        }
        printf("\n");
    }

    return 0;
}# desafio-batalha-naval-gabyelidio
