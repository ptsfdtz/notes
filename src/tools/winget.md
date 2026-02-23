# winget

window提供的包管理工具，类似于apt-get、yum等。

### 更新

1. 查看winget源

```sh
winget source list
```

2. 更新源

```sh
winget source update
```

3. 更新软件

```sh
winget upgrade --all
```

### 常用软件

- vscode

```sh
winget install --id Microsoft.VisualStudioCode -s winget
```

- git

```sh
winget install --id Git.Git -s winget
```

- chrome

```sh
winget install --id Google.Chrome -s winget
```

- 7zip

```sh
winget install --id 7zip.7zip -s winget
```

- JLC EDA Pro

```sh
winget install --id JLC.LCEDA.Pro -s winget
```

- arduino

```sh
winget install --id ArduinoSA.IDE.stable -s winget
```

- bandizip

```sh
winget install --id Bandisoft.Bandizip -s winget
```

- draw.io

```sh
winget install --id JGraph.Draw io.Desktop -s winget
```

- obs-studio

```sh
winget install --id OBSProject.OBSStudio -s winget
```

- telegram

```sh
winget install --id Telegram.TelegramDesktop -s winget
```

- nano

```sh
winget install --id okibcn.nano -s winget
```

- vim

```sh
winget install --id vim.vim -s winget
```

- wireguard

```sh
winget install --id WireGuard.WireGuard -s winget
```

- QQ

```sh
winget install --id Tencent.QQ -s winget
```

- wechat

```sh
winget install --id Tencent.WeChat -s winget
```
