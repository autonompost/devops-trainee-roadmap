# General Informations about Linux CLI Editors

On most Linux distributions the default editor can be changed by using the following command. This will open up a menu which lets you select which editor to use.
```shell
sudo update-alternatives --config editor
```

The default editor settings can be checked by using
```shell
sudo update-alternatives --query editor
```

On **Redhat based systems** the default editor can be changed by:
```shell
sudo alternatives --config editor
```

And displayed by
```shell
sudo alternatives --display editor
```

