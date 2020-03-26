# Workers_Redirect
利用CloudFlare的Workers来URL重定向

## 用途

该脚本是利用CloudFlare的Workers来进行URL重定向，用途可以自行发掘。目前我用它来做自己站点的快捷入口和AFF邀请链接跳转。 演示站点 33.al

## 使用方法

1. 建立一个JSON文件存放我们的跳转URL

   内容为

   ```json
   {
   	"kms": "http://kms.i5.gs/",
   	"donate": "http://pinqiong.net/",
   	"a/dynadot": "http://www.dynadot.com/?s9B17C8l9D6W6E7K",
   	"a/qcloud": "https://url.cn/5hKENDf"
   }
   ```

   很明显，JSON里面存放的是键值对，前面的是访问URL，后面的是跳转的URL

   比如我访问 `33.al/kms` ，就会跳转到 `http://kms.i5.gs/`。注意前者中不能出现?或者#，如果需要中文的话，需要URL编码。

2. 编辑我们的`index.js`

   我们需要修改index.js中的第15行

   ```javascript
   var url = "https://raw.githubusercontent.com/yumusb/cdn/master/cloudflare/redirect.json"
   ```

   ** 这里一定是JSON文件的真实地址，推荐放到github。例如我的是放在这里 <https://github.com/yumusb/cdn/blob/master/cloudflare/redirect.json>（下载链接为<https://raw.githubusercontent.com/yumusb/cdn/master/cloudflare/redirect.json> 可以在GIthub的文件页面点击右上角`raw`获得），*

   第24行

   ```javascript
   url = 'https://huai.pub'
   ```

   ** 这里是默认的跳转地址，如果上面的JSON文件中没有这个路由，就问跳转到默认页面 。*

3. 部署到CloudFlare的Workers

   如果你使用过其他workers脚本，相信这一步对你很简单。

   如果没用过，可以从这里获得帮助 <https://workers.cloudflare.com/>