# newhorizons

Protótipo mínimo de um blog pessoal utilizando **Jekyll + GitHub Pages**.

O objetivo deste repositório é demonstrar e validar como o ecossistema estático funciona de ponta a ponta — sem temas prontos, sem frameworks CSS/JS e sem abstrações desnecessárias.

---

## 1. O que é o Jekyll neste projeto?

O **Jekyll** é um **gerador de sites estáticos (Static Site Generator - SSG)**. 

Em vez de usar um servidor com banco de dados (como WordPress ou Django) que processa páginas a cada requisição, o Jekyll roda previamente: ele lê arquivos de texto em Markdown (`.md`), passa pelo motor de templates **Liquid**, injeta o conteúdo nos layouts HTML (`_layouts/`) e gera páginas HTML puras prontas para serem servidas.

### O Fluxo de Transformação

```text
Markdown (texto simples com front matter)
   ↓
Jekyll (processa Liquid, aplica layouts e gera HTML)
   ↓
HTML (arquivos estáticos em _site/)
   ↓
GitHub Pages (servidor HTTP estático do GitHub)
   ↓
Browser (o visitante consome HTML/CSS nativo)
```

---

## 2. Onde ficam os posts?

Todos os posts ficam na pasta:

```text
_posts/
```

O Jekyll exige a seguinte convenção para o nome do arquivo:
```text
AAAA-MM-DD-titulo-do-post.md
```

* **Data no nome do arquivo:** determina a data padrão de ordenação e geração do link.
* **Slug:** o texto após a data vira parte da URL do post.

---

## 3. Como criar um novo post?

1. Crie um novo arquivo em `_posts/` seguindo a convenção de data:
   Exemplo: `_posts/2026-09-19-segundo-post.md`

2. Adicione o cabeçalho **Front Matter** (delimitado por `---`) no início do arquivo:
   ```yaml
   ---
   layout: post
   title: "Título do seu post"
   date: 2026-09-19
   ---
   ```

3. Escreva o conteúdo em Markdown comum logo abaixo do cabeçalho:
   ```markdown
   Este é o conteúdo do post escrito em Markdown puro.
   ```

---

## 4. Como rodar localmente?

### Instalar dependências:
```bash
bundle install
```

### Iniciar o servidor local:
```bash
bundle exec jekyll serve
```

Acesse no navegador:
```text
http://localhost:4000
```

### Com recarregamento automático (LiveReload):
Para que o navegador atualize automaticamente sempre que você salvar um arquivo:
```bash
bundle exec jekyll serve --livereload
```

---

## 5. Como funciona o build?

Para gerar apenas os arquivos estáticos sem iniciar o servidor:

```bash
bundle exec jekyll build
```

* O Jekyll lê todos os arquivos do projeto e compila o site final dentro da pasta:
  ```text
  _site/
  ```
* É nessa pasta `_site/` que ficam os arquivos `.html`, as folhas `.css` e as imagens finais.
* **Nota:** A pasta `_site/` está listada no `.gitignore` e **nunca** deve ser enviada ao Git.

---

## 6. Como publicar no GitHub Pages?

O GitHub Pages possui integração nativa com o Jekyll. Quando você envia seu código para o repositório, o GitHub detecta o `_config.yml` e o `Gemfile` e executa o build automaticamente.

### Passo a passo:

1. **Inicialize o repositório Git e faça o commit:**
   ```bash
   git init
   git add .
   git commit -m "feat: prototipo inicial do blog newhorizons"
   ```

2. **Crie o repositório no GitHub** com o nome `newhorizons`.

3. **Conecte e envie para o GitHub:**
   ```bash
   git branch -M main
   git remote add origin https://github.com/SEU-USUARIO/newhorizons.git
   git push -u origin main
   ```

4. **Ativar o GitHub Pages no repositório:**
   * No GitHub, acesse: **Settings** > **Pages**.
   * Em **Build and deployment** > **Source**, mantenha **Deploy from a branch**.
   * Em **Branch**, selecione `main` e a pasta `/(root)`.
   * Clique em **Save**.

5. **Ajuste de URL do projeto (se necessário):**
   * Se a URL do seu site for `https://SEU-USUARIO.github.io/newhorizons`, abra o `_config.yml` e ajuste:
     ```yaml
     baseurl: "/newhorizons"
     ```
   * Envie o commit da alteração (`git commit -am "fix: ajusta baseurl" && git push`).

O GitHub executará o build automaticamente e em poucos segundos seu blog estará no ar!
