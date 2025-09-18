before installing oh-my-posh install oh-my-zsh

after that .local/bin is not exported so add this command at the very beginning in .zshrc file
`export PATH=$PATH:/home/anurag/.local/bin`

then add this eval "$(oh-my-posh init zsh)" 

then execute `oh-my-posh --version` to check if oh-my-posh was installed 

`oh-my-posh font install meslo` for installing fonts

### Set Theme
REMEMBER: In new documentation the option for installing all the themes has been removed. So use these command or else you might get "CONFIG ERROR"

``` bash
mkdir -p ~/.poshthemes
```

```bash
curl -sL https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/themes.zip -o ~/.poshthemes/themes.zip
```

```bash
unzip ~/.poshthemes/themes.zip -d ~/.poshthemes
```

```bash
rm ~/.poshthemes/themes.zip
```

and then add the line to .zshrc file: 
```.zshrc
eval "$(oh-my-posh init bash --config ~/.poshthemes/<theme-name>.omp.json)"
```

then restart terminal
#### Configuring Any Theme
Now, create a folder inside .config folder with name "ohmyposh"
then export the folder with 
```bash
oh-my-posh config export --output ./base.json
```
