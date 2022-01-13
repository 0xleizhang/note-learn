ConfigMap
\`\`\`
apiVersion: v1
kind: ConfigMap
metadata:
 name: game-demo
data:
 # 类属性键；每一个键都映射到一个简单的值
 player\_initial\_lives: "3"
 ui\_properties\_file\_name: "user-interface.properties"

 # 类文件键
 game.properties: \| \\\换行文件类型
 enemy.types=aliens,monsters
 player.maximum-lives=5
 user-interface.properties: \|
 color.good=purple
 color.bad=yellow
 allow.textmode=true
\`\`\`

Secret 加密信息
\`\`\`
apiVersion: v1
kind: Secret
metadata:
 namespace: prow
 name: hmac-token
stringData: //stringData能够保存任意信息，如果data字段必须base64加密
 # Generate via \`openssl rand -hex 20\`. This is the secret used in the GitHub webhook configuration
 hmac: << insert-hmac-token-here >>
\`\`\`