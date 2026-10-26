# StapVpSim — distribuição ofuscada

Contém apenas o bundle ofuscado e seu carregador. O repositório de desenvolvimento é mantido separadamente.

## Carregar

```lua
loadstring(game:HttpGet("https://raw.githubusercontent.com/rhgab1/StapVpSim-obfuscated/main/TutorialAutopilot.bundle.lua"))()
```

O comportamento original foi preservado: carregar manualmente prepara o controlador e o deixa pausado. Para iniciar o fluxo:

```lua
shared.TapSimulatorTutorialAutopilot:Start()
```

Para parar:

```lua
shared.TapSimulatorTutorialAutopilot:Stop()
```

## Compatibilidade e limites

- Requer ambiente Luau com as APIs usadas no projeto original, incluindo `game:HttpGet`, `loadstring`, `setfenv` e `bit32`.
- A retomada após teleport mantém a dependência original dos arquivos locais `mcp/StapVpSimTutorialAutopilot.manifest` e suas partes; este carregamento por URL não instala esses arquivos.
- A ofuscação renomeia variáveis e funções locais, remove comentários e codifica o conteúdo. Ela dificulta a leitura, mas não impede a recuperação do código nem protege segredos.
- Os 19 módulos, o bundle e o carregador foram compilados com Luau. O decodificador foi testado byte a byte, incluindo argumentos, retornos e erros.
- O teste offline `Test-StepTracker.luau` do projeto original já falha na linha 55; a versão transformada apresenta a mesma falha. Não houve teste dentro do Roblox.

Ferramenta de transformação: [darklua](https://darklua.com/docs/rules/rename_variables/).
