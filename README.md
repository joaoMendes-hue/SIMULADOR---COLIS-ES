# Simulação de Colisões entre Esferas

## Descrição

Este projeto implementa uma simulação computacional de colisões elásticas entre esferas ("bolas de sinuca") em duas dimensões utilizando Python e Pygame.

As esferas possuem posições e velocidades iniciais aleatórias e se movimentam dentro de uma região retangular limitada por paredes. Durante a simulação, são detectadas e tratadas colisões entre as esferas e entre as esferas e as paredes, atualizando suas velocidades de acordo com as leis da mecânica clássica.

O objetivo é demonstrar conceitos de dinâmica, conservação da quantidade de movimento e colisões elásticas por meio de uma visualização gráfica em tempo real.

---

## Funcionalidades

* Simulação em tempo real.
* Inicialização aleatória das posições das esferas.
* Inicialização aleatória das velocidades.
* Colisões elásticas entre esferas.
* Colisões com as paredes da janela.
* Atualização contínua das posições utilizando integração numérica.
* Interface gráfica desenvolvida com Pygame.

---

## Fundamentos Físicos

A posição de cada esfera é atualizada a cada intervalo de tempo Δt segundo:

x(novo) = x(atual) + vx · Δt

y(novo) = y(atual) + vy · Δt

onde:

* x e y representam as coordenadas da esfera;
* vx e vy representam as componentes da velocidade;
* Δt representa o passo temporal da simulação.

As colisões são consideradas perfeitamente elásticas, preservando:

* Quantidade de movimento;
* Energia cinética.

---

## Estrutura do Projeto

```text
simulacao-colisoes/
│
├── simulacao.py
├── README.md
└── requirements.txt
```

---

## Requisitos

* Python 3.11 ou superior
* Pygame

---

## Instalação

Clone o repositório:

```bash
git clone https://github.com/SEU_USUARIO/simulacao-colisoes.git
```

Entre na pasta:

```bash
cd simulacao-colisoes
```

Instale as dependências:

```bash
python -m pip install pygame
```

---

## Execução

Execute o programa com:

```bash
python simulacao.py
```

Ao iniciar, uma janela será aberta automaticamente e a simulação começará imediatamente.

---

## Parâmetros da Simulação

Os principais parâmetros podem ser modificados diretamente no código:

| Parâmetro | Descrição                        |
| --------- | -------------------------------- |
| WIDTH     | Largura da janela                |
| HEIGHT    | Altura da janela                 |
| N_BOLAS   | Número de esferas                |
| RAIO      | Raio das esferas                 |
| FPS       | Taxa de atualização da simulação |

---

## Algoritmo Utilizado

Para cada passo da simulação:

1. Atualizar a posição de cada esfera.
2. Verificar colisões com as paredes.
3. Verificar colisões entre pares de esferas.
4. Atualizar as velocidades das esferas envolvidas.
5. Corrigir eventuais sobreposições.
6. Redesenhar a cena na janela.

A detecção de colisões entre esferas utiliza a distância entre os centros das partículas.

---

## Complexidade Computacional

A verificação de colisões entre esferas é realizada comparando todos os pares possíveis.

Complexidade:

```text
O(N²)
```

onde N é o número de esferas presentes na simulação.

---

## Tecnologias Utilizadas

* Python
* Pygame
* Matemática Vetorial
* Mecânica Clássica

---

## Possíveis Melhorias

* Simulação em 3D.
* Diferentes massas para as esferas.
* Controle de atrito.
* Interface para alteração de parâmetros.
* Leitura de configurações por arquivo externo.
* Otimização da detecção de colisões para grandes quantidades de partículas.

---

## Autor

Nome: João Victor Mendes De Oliveira 

Disciplina: Física 1 / Simulação de Sistemas Físicos

Instituição: UTFPR

Ano: 2026

