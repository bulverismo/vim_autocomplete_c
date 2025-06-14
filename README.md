certifique vim maior que  Vim >= 9.0.0438
Install nodejs >= 16.18.0

vim --version


```
#install vim
wget https://github.com/vim/vim/archive/refs/tags/v9.1.1457.tar.gz -O vim.tar.gz
tar --extract --file vim.tar.gz
cd vim*
make -j$(nproc)
sudo make install

#install node
curl -sL install-node.vercel.app/lts | sudo bash

#instalar gerenciador de plugins vim plug
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

```

instale no vim o coc

https://github.com/neoclide/coc.nvim

```
# adicione isso ao ~/.vimrc
call plug#begin()

    Plug 'neoclide/coc.nvim', {'branch': 'release'}

call plug#end()

Depois digite nos comandos do vim :PlugInstall e confirme a instalação com y

depois adicione os comandos do coc básico, tem no github deles, legal ver o atual la e trazer por conta da versão poder ter situações especificas

instalar dentro do vim através do coc o suporte ao clangd que é o que vai fazer ter o autocomplete básico do c

https://github.com/clangd/coc-clangd

vim -c "CocInstall coc-clangd"

voce vai ter que sair do vim apos a instalação com :q


instalar ccls
sudo apt install ccls

descubra a versão do clangd para por no arquivo de configuração do coc
vai ser algo assim
ls ~/.config/coc/extensions/coc-clangd-data/install/15.0.6/clangd_15.0.6/bin/clangd

coloque isso no seu CocConfig
RESPEITANDO A VERSÃO DO CLANGD
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


instale o compiledb, que será o cara que gera o arquivo compile_commands.json
https://github.com/nickdiego/compiledb?tab=readme-ov-file

no projeto faça algo como: 
compiledb make
compiledb gcc -o .... -lm ..

e assim vai gerar o compile_commands que será necessário pro autocomplete ficar legal, funcionando inclusive para libs que tu mesmo programar



```
