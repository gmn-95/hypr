# Configuração do Hyprland

Backup versionado da minha configuração do [Hyprland](https://hypr.land/) em `~/.config/hypr`.

O foco deste repositório é preservar o comportamento do compositor, atalhos, bloqueio de tela, inatividade e a configuração dos monitores. Ele não inclui configurações de aplicativos mantidas em outros diretórios, como Waybar, Rofi ou Kitty.

## Conteúdo

| Arquivo | Finalidade |
| --- | --- |
| `hyprland.lua` | Configuração principal: aparência, comportamento, regras de janela, inicialização e atalhos. |
| `monitors.lua` | Layout ativo dos monitores. É carregado ao final de `hyprland.lua`. |
| `monitors.conf` | Snapshot gerado pelo `nwg-displays`; não é carregado pela configuração Lua atual. |
| `hyprlock.conf` | Tela de bloqueio no estilo Catppuccin Mocha. |
| `wallpapers/hyprlock-catppuccin-aurora.png` | Fundo usado pelo Hyprlock. |
| `hypridle.conf` | Bloqueia após 10 minutos e desliga os monitores após 15 minutos. |
| `hyprbuntu-binds.lua` | Atalhos adicionais mantidos como referência para o ambiente Hyprbuntu. |
| `workspaces.conf` | Espaço reservado para regras de workspaces. |

## Dependências

Além do Hyprland com suporte à configuração Lua, esta configuração usa os programas abaixo. Instale somente os que correspondem aos recursos que você deseja manter.

| Recurso | Programas usados |
| --- | --- |
| Bloqueio e inatividade | `hyprlock`, `hypridle` |
| Terminal, arquivos e menu | `kitty`, `nautilus`, `rofi` |
| Notificações | `swaync` |
| Capturas de tela | `grim`, `slurp`, `swappy`, `hyprshot` |
| Área de transferência | `copyq` |
| Barra reiniciada pelo atalho de recarga | `waybar` |

Dois caminhos externos devem existir ou ser ajustados em `hyprland.lua` antes de usar a configuração em outra máquina:

- `~/.config/rofi/launchers/type-4/launcher.sh`
- `~/.local/bin/hyprshot`

## Instalação em uma máquina nova

> Atenção: os arquivos de monitor deste repositório descrevem os conectores e as resoluções da minha mesa. Edite `monitors.lua` antes de recarregar o Hyprland em outro computador.

Faça uma cópia da configuração atual e clone o repositório no local esperado pelo Hyprland:

```bash
mv ~/.config/hypr ~/.config/hypr.backup
git clone git@github.com:gmn-95/hypr.git ~/.config/hypr
```

Para usar HTTPS, troque a URL de clone pela URL HTTPS exibida pelo GitHub. Depois, ajuste os monitores conforme as saídas disponíveis:

```bash
hyprctl monitors
$EDITOR ~/.config/hypr/monitors.lua
```

Com uma sessão Hyprland aberta, aplique as mudanças:

```bash
hyprctl reload
```

## Atalhos principais

| Atalho | Ação |
| --- | --- |
| `Super + T` | Abre o Kitty. |
| `Super + E` | Abre o Nautilus. |
| `Super + R` | Abre o launcher do Rofi. |
| `Super + Shift + R` | Recarrega o Hyprland e reinicia o Waybar. |
| `Super + L` | Bloqueia a sessão com Hyprlock. |
| `Super + N` | Abre o painel de notificações. |
| `Super + P` | Captura uma região e abre no Swappy. |
| `Super + 1` até `0` | Alterna entre workspaces. |
| `Super + Shift + 1` até `0` | Move a janela para outro workspace. |

Consulte `hyprland.lua` para a lista completa, incluindo movimentação e redimensionamento de janelas com mouse.

## Hyprlock

A tela de bloqueio usa a paleta Catppuccin Mocha, a fonte `JetBrainsMono Nerd Font` e o wallpaper incluído neste repositório. O comando abaixo bloqueia a sessão de verdade; salve seu trabalho antes de executá-lo:

```bash
hyprlock
```

## Mantendo o backup atualizado

Após alterar uma configuração, revise e envie a mudança para o GitHub:

```bash
git status
git add hyprland.lua hyprlock.conf hypridle.conf monitors.lua hyprbuntu-binds.lua workspaces.conf wallpapers/
git commit -m "atualiza configuracao do Hyprland"
git push
```

Antes de começar a editar em outra máquina, atualize a cópia local:

```bash
git pull --ff-only
```
