# JogoDaVelha

Teste Prático - DTI
Enunciado Geral
O objetivo deste projeto é desenvolver uma api para um jogo multiplayer de Jogo da Velha.
Tempo Estimado: 24 horas de prazo
Premissas
Poderá ser feito em qualquer linguagem;
Deverá conter um README com instruções claras de build e dependências;
Build automatizado é opcional mas desejável;
Não pode haver dependência de banco de dados ou serviços externos. A persistência dos dados pode
ser feita por exemplo in-memory ou baseada em arquivos;
Não é necessária preocupação com autenticação dos métodos;
Será avaliado além do funcionamento da API boas práticas de desenvolvimento de software.
Detalhes
A api deverá conter os métodos abaixo. O funcionamento da partida será baseado em turnos, a cada
momento um jogador realiza a jogada.
POST - /game
Essa chamada criara uma nova partida e retornará o id da partida criada. Além do id ele vai sortear qual
jogador ira começar a partida o "X" ou o "O".
Exemplo de returno:
{
 "id" : "fbf7d720-df90-48c4-91f7-9462deafefb8",
 "firstPlayer": "X"
}
POST - /game/{id}/movement
Essa chamada fará o movimento de cada jogador.
Input:
{
 "id" : "fbf7d720-df90-48c4-91f7-9462deafefb8",
 "player": "X",
 "position": {
 "x": 0,
 "y": 1


 }
}
As coordenadas X e Y representam a posição no tabuleiro do movimento. Começando do índice 0, no canto
inferior esquerdo. De forma que o tabuleiro fica assim:

(x=0 y=2) | (x=1 y=2) | (x=2 y=2)
----------|-----------|----------
(x=0 y=1) | (x=1 y=1) | (x=2 y=1)
----------|-----------|----------
(x=0 y=0) | (x=1 y=0) | (x=2 y=0)

O player representa o jogador que está fazendo a jogada. Esse input por exemplo criaria a jogada abaixo:
Caso a jogada seja feita com sucesso o código 200 deve ser retornado.
Caso não seja o turno do jogador, ou a partida não exista, um erro deve ser retornado.
Retorno:
Turno Errado


{
 "msg": "Não é turno do jogador"
}
Partida Inexistente
{
 "msg": "Partida não encontrada"
}
Finalmente se o jogo chegar ao fim o retorno deve ser assim:
{
 "msg": "Partida finalizada",
 "winner": "X"
}
Se o jogo deu velha (empate), o campo jogador ganhador deve vir preenchido da seguinte forma:
{
 "status": "Partida finalizada",
 "winner": "Draw"
}
