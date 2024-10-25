---
aliases:
  - "Classe: Player"
---
Um objeto Player é um cliente que esteja conectado atualmente. É adicionado quando um novo jogador se conecta, e então removido quando eles saem do servidor.
Com ele, temos informações universais sobre o jogador, como nome, lista de amigos, e etc, além de informações e propriedades relacionadas ao ciclo de vida de um jogador (entre entrar e sair da experiência).
Cada objeto Player é pai de 4 containeres importantes: Backpack, StarterGear, PlayerGui e PlayerScripts 

O nome do objeto Player reflete o username do jogador. Quando salvamos informações de um jogador, usamos a informação `Player.UserId`, pois este identificador é fixo.

Para trabalhar com objetos Player, devemos usar estes metodos ao invés dos seus métodos de Instance:
- Para pegar uma table dos jogadores atuais, usamos `Players:GetPlayers()`. Para jogadores, usamos isso ao invés de `Instance.GetChildren()`;
- Para detectar a adição de jogadores, é recomendado usar o evento `Players.PlayerAdded` ao invés de `Instance.ChildAdded` no serviço de Players;
- Detectamos a remoção de objetos Player usando `Players.PlayerRemoving`, que é disparado **antes** do jogador sair. Importante caso esteja salvando informações do jogador na saída.

> Documentação do objeto [Player](https://create.roblox.com/docs/reference/engine/classes/Player)


## Ciclo de vida
Tanto o client quanto o servidor podem se conectar aos eventos `Players.PlayerAdded` e `Player.PlayerRemoved`. Eles também podem se conectar aos eventos `Player.CharacterAdded`, `Player.CharacterRemoving` e `Humanoid.Died`.
Usamos Scripts para acessar serviços server-side, como armazenamentos para obter dados salvos do jogador. Usamos LocalScripts se o client precisar criar e remover instâncias de gameplay relacionadas ao usuário novo, como um GUI.

Exemplos de utilidade para o evento `Players.PlayerAdded`:
- Carregar dados salvos de um jogador;
- Atribuir uma equipe;
- Mudar a roupa de um personagem;

Exemplos de uso para o evento `Players.PlayerRemoving`:
- Salvar dados do usuário;
- Remover dados do placar;
- Destruir modelos relacionados a ele, como uma casa;

# Backpack
O container `Player.Backpack` é o inventário do usuário. Os objetos `Tools` que estejam no inventário são exibidos na barra de baixo da tela. Se um usuário seleciona alguma Tool, ele equipa e ela se move da Backpack para `Player.Character`.
Quando um `Player.Character` nasce, o conteúdo de `Player.StarterGear` é clonado para sua Backpack. Quando o jogador morre, o client destrói sua Backpack e substitui por uma nova.
A Backpack também guarda Scripts e LocalScripts que tanto o servidor quando o client podem acessar.
Para desabilitar a interface padrão do Roblox para as ferramentas, use `StarterGui:SetCoreGuiEnabled()` com sua interface padrão em um LocalScript.

# StarterGear