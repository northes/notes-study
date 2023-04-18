## 示例配置

配置服务器多个一定要配置 `context`指定不同的本地路径, 否则只会显示最后一个服务器

`.vscode/sftp.json`

```json
[
    {
        "name": "MK Mini Game",
        "protocol": "sftp",
        "port": 10022,
        "username": "root",
        "uploadOnSave": false,
        "useTempFile": false,
        "openSsh": true,
        "remotePath": "/root/app",
        "privateKeyPath": "/Users/mac/.ssh/id_rsa",
        "host": "mk.mini.prod.ecs.game.1.littlehero.xyz",
        "defaultProfile": "prod",
        "context": "./mk_qq_mini_game"
    },
    {
        "name": "MK Mini Shared",
        "protocol": "sftp",
        "port": 10022,
        "username": "root",
        "uploadOnSave": false,
        "useTempFile": false,
        "openSsh": true,
        "remotePath": "/root/app",
        "privateKeyPath": "/Users/mac/.ssh/id_rsa",
        "host": "mk.mini.prod.ecs.shared.1.littlehero.xyz",
        "defaultProfile": "prod",
        "context": "./mk_qq_mini_shared"
    }
]```