# Configuração do Vim para Autocompletar em C com CoC

>  **Requisitos**  
- Vim >= **9.0.0438**  
- Node.js >= **16.18.0**  

Verifique a versão do Vim com:

```bash
vim --version
```

---

##  Instalação

### 1. Instalar o Vim

```bash
wget https://github.com/vim/vim/archive/refs/tags/v9.1.1457.tar.gz -O vim.tar.gz
tar --extract --file vim.tar.gz
cd vim*
make -j$(nproc)
sudo make install
```

---

### 2. Instalar o Node.js (LTS)

```bash
curl -sL install-node.vercel.app/lts | sudo bash
```

---

### 3. Instalar o gerenciador de plugins [vim-plug](https://github.com/junegunn/vim-plug)

```bash
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
     https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

---

##  Configurar CoC (Conquer of Completion)

### 1. Adicionar ao `~/.vimrc`:

```vim
call plug#begin()

    Plug 'neoclide/coc.nvim', {'branch': 'release'}

call plug#end()
```

> Em seguida, abra o Vim e execute:  
> `:PlugInstall`  
> Confirme com `y` quando solicitado.

---

### 2. Instalar extensão `coc-clangd` para C/C++

```bash
vim -c "CocInstall coc-clangd"
```

> Após a instalação, saia do Vim com `:q`

---

##  Configurar o CoC para usar `clangd` e `ccls`

### 1. Instalar o `ccls`

```bash
sudo apt install ccls
```

### 2. Descubra a versão instalada do `clangd`

```bash
ls ~/.config/coc/extensions/coc-clangd-data/install/*/clangd_*/bin/clangd
```

Copie o caminho exato da versão instalada.

---

### 3. Editar o arquivo `:CocConfig`

Exemplo de configuração (ajuste o caminho do `clangd` conforme sua versão):

```json
{
  "languageserver": {
    "ccls": {
      "command": "ccls",
      "args": ["--log-file=/tmp/ccls.log", "-v=1"],
      "filetypes": ["c", "cc", "cpp", "c++", "objc", "objcpp"],
      "rootPatterns": [".ccls", "compile_commands.json"],
      "initializationOptions": {
        "cache": {
          "directory": "/tmp/ccls"
        },
        "client": {
          "snippetSupport": true
        }
      }
    }
  },
  "clangd.path": "~/.config/coc/extensions/coc-clangd-data/install/15.0.6/clangd_15.0.6/bin/clangd"
}
```

---

##  Gerar `compile_commands.json` com `compiledb`

### 1. Instale o [compiledb](https://github.com/nickdiego/compiledb)

Siga as instruções do repositório para instalar.

### 2. Use no seu projeto:

```bash
compiledb make
# ou
compiledb gcc -o programa arquivo.c -lm
```

Esse arquivo (`compile_commands.json`) será usado pelo `ccls` e `clangd` para fornecer autocomplete inteligente, incluindo suporte a bibliotecas criadas por você.

---

 Agora o Vim está configurado para autocomplete em C com suporte a bibliotecas.
