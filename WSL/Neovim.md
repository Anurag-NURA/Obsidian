First to remove or uninstall already installed Neovim in your system

After that go to https://github.com/neovim/neovim/releases
1. Download .tar or .appimage of the neovim version you want to install
2. Extract it:
```bash
tar -xvzf nvim-linux-x86_64.tar.gz
```

3. Move the `nvim` binary to a directory in your PATH, for example:

```bash
sudo cp ~/win_home/nvim-linux-x86_64/bin/nvim /usr/local/bin/
```

4. Verify the installation:
```bash
nvim --version
```

### Optional:
Then make it executable
```bash
chmod +x ~/.local/bin/nvim
```

Add to PATH 
```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
```

```bash
source ~/.zshrc
```
