# StapVpSim — arquivo único ofuscado

`TutorialAutopilot.bundle.lua` contém os 19 módulos, o início automático e a retomada por URL. Toda essa implementação está no arquivo ofuscado. O repositório privado de desenvolvimento permanece separado e não foi alterado.

## Executar

```lua
loadstring(game:HttpGet("https://raw.githubusercontent.com/rhgab1/StapVpSim-obfuscated/main/TutorialAutopilot.bundle.lua"))()
```

Esse único comando carrega o controlador e inicia o fluxo assim que perfil, personagem e mapa estiverem prontos. Também é possível executar diretamente o conteúdo do arquivo Lua no ambiente compatível. Não é necessária uma chamada separada de `Start()`.

## Troca de servidor

Quando o executor oferece `queue_on_teleport`, `queueonteleport` ou `queue_on_tp`, o arquivo arma a retomada. Depois da troca, aguarda 30 segundos e baixa novamente este mesmo arquivo pela URL pública. São até seis tentativas, com cinco segundos entre elas. Não depende de manifesto nem de partes salvas no disco. Sem suporte à fila, execute novamente o comando após a troca.

Para parar manualmente:

```lua
shared.TapSimulatorTutorialAutopilot:Stop()
```

## Compatibilidade e validação

- Requer ambiente Luau com as APIs do projeto, incluindo `game:HttpGet`, `loadstring`, `setfenv` e `bit32`. A retomada também requer conexão à internet e suporte à fila de teleport.
- A lógica dos 19 módulos de jogo foi preservada. Apenas o início e o carregamento após teleport foram adaptados para a distribuição em arquivo único.
- Compilação, equivalência das instruções dos módulos e decodificação byte a byte foram verificadas. Início automático, espera pela prontidão, substituição da execução anterior e retomada com falhas de rede/compilação/execução foram testados com simulação local.
- O teste offline `Test-StepTracker.luau` original já falha na linha 55; a transformação mantém a mesma falha. Não houve novo teste dentro do Roblox.
- Ofuscação dificulta a leitura, mas não impede recuperar o código nem protege segredos.

Ferramenta de transformação: [darklua](https://darklua.com/docs/rules/rename_variables/).
