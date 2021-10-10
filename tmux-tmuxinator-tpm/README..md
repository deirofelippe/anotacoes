# Tmux e Tmuxinator

## Conteudos

- [](#)
- [](#)
- [](#)

## Tmux, tpm e tmuxinator

- Tmux: cria vários terminais dentro de um só (sessão). Esses terminais são divididos em janelas e paineis.
- Tmuxinator: gerenciador de sessoes, janelas e paineis. É possivel criar um manifesto que quando executado, cria automaticamente todo um ambiente de trabalho desejado.
- TPM: gerenciador de plugins para o tmux.

## Tmux

- `tmux new -s [nome-sessao]`: coloca nome 'demo' na sessao
- `tmux ls`: lista sessões criadas
- `tmux attach -t [nome-sessao]`: abre a sessao de nome 'demo'
- `tmux kill-server`: fecha todas as sessões
- `tmux kill-session -t [nome-sessao]`: fecha uma sessão específica

exit (sai na seguinte ordem: painel, janela e sessão)

- SESSÃO
	- <c-b>d (sair da sessao sem deletar)
	- <c-b>s (listar sessões)
	- <c-b>$ (renomear)
	- <c-b>?
- JANELA
	- <c-b>c (nova janela)
	- <c-b>& (deleta a janela atual)
	- <c-b>, (renomear janela atual)
	- <c-b><numero> (abre a janela do numero digitado)
- PAINEL
	- <c-b>" (cria painel horizontalmente)
	- <c-b>% (cria painel verticalmente)
	- <c-b>x (fechar painel)
	- <c-b>q (mostra indice de tds os paineis da janela)
	- <c-b><seta> (muda pro painel na direcao da seta)
	- <c-b>[ (copy mode)
	- q (sair do copy mode)

- <c-b><seta> (modifica tamanho do painel)
	OBS: aperte a seta sem soltar o <c-b>, se soltar por um tempo a seta, o comando nao funcionara

## Tmuxinator

- aliases
	- open as o
	- new as n
	- edit as e
	- copy as cp
	- delete as rm
	- start as s

- tmuxinator new [nome-projeto] (fica salvo em '~/.config/tmuxinator')
- tmuxinator new --local [nome-projeto] (fica salvo no diretorio atual)
- tmuxinator open [nome-projeto]
- tmuxinator open --local [nome-projeto]

- tmuxinator [nome-projeto]
- tmuxinator start [nome-projeto]
- tmuxinator start [nome-projeto] -n [nome] -p [project-config]

- tmuxinator copy [existente] [novo]
- tmuxinator list
- tmuxinator delete [nome-projeto]
- tmuxinator help

### Exemplo de .yaml

```yaml
name: dev
root: ~/<%= @args[0] %>

windows:
  - dev:
      pre:
        - echo "a"
      layout: main-vertical
      panes:
        - echo "a" 
        - echo "a"
        - echo "a"
        - pane_with_multiple_commands:
            - clear
  - git:
      layout: tiled
      pre:
        - echo "a"
      panes:
        - echo "a"
        - echo "a"
  - ht:
    - htop
```
