# pr-assets — imagens e mídia dos nossos PRs

Branch **órfã**. Não tem ancestral comum com `main` e **nunca deve ser mergeada
em lugar nenhum**. Existe só para hospedar arquivo binário (screenshot, GIF,
vídeo curto) que a gente linka na descrição de PR e issue, sem sujar a árvore
do upstream.

Repo é fork de `KroxiLabs/Kroxitrade`. Regra do local-context vale aqui:
nada nosso entra em arquivo rastreado da `main`. Mídia de PR é "nossa" — por
isso mora aqui, isolada.

## Regras

1. **Nunca** `git merge pr-assets` em `main` nem em branch de feature.
2. **Nunca** incluir esta branch em PR pro upstream. Ela vive só no nosso fork
   (`origin` = `JohnsonMauro/Kroxitrade`).
3. Só binário de mídia e este README. Nada de código.
4. Não reescrever história aqui — URL já colada em PR quebra.
5. Arquivo é imutável: para corrigir uma imagem, sobe outra com nome novo.

## Layout

```
<numero-ou-slug-do-pr>/
  antes.png
  depois.png
  demo.gif
```

Sem número de PR ainda? Usa o slug da branch:
`bookmark-folder-icon-picker/depois.png`.

## Como subir sem trocar de branch

Working tree fica na `main`; usa worktree separado:

```bash
git worktree add ../Kroxitrade.pr-assets pr-assets
cp ~/shot.png ../Kroxitrade.pr-assets/91-quick-filters/depois.png
cd ../Kroxitrade.pr-assets
git add . && git commit -m "assets: screenshots do PR #91"
git push origin pr-assets
cd -
git worktree remove ../Kroxitrade.pr-assets
```

## URL para colar no PR

```
https://raw.githubusercontent.com/JohnsonMauro/Kroxitrade/pr-assets/<caminho>
```

Em markdown:

```markdown
![depois](https://raw.githubusercontent.com/JohnsonMauro/Kroxitrade/pr-assets/91-quick-filters/depois.png)
```

`raw.githubusercontent.com` serve o arquivo direto e funciona em PR do upstream,
porque o fork é público. Link de `github.com/.../blob/...` renderiza página, não
imagem — não usar.

## Peso

Manter screenshot em PNG otimizado ou WebP. Evitar vídeo grande: branch órfã
ainda conta no tamanho do clone de quem der `fetch --all`. Acima de ~2 MB,
preferir upload direto na caixa de comentário do GitHub.
