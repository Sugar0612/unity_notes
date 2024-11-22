WebGL打开后有一段预加载，通常都比较慢，很多甲方要求一分钟内打开，所以需要优化，以下几点时我做项目时的优化心得:
1. 项目预加载时会执行脚本中的'Awake()' 所以Awake中只进行初始化操作，剩下的尽量放在Start里面。
2. 减少资源的体积大小，包体太大也会影响加载速度，所以合理的缩小Resources中的体积，也可以加快速度。具体可以看[FBX文件优化](../../Resources/LoadFBX.md)。
3. IIS配置优化，多数WebGL打包使用的是gzip打包方法，然后会搭在IIS服务器上，可以让IIS对gzip进行快速解包。在项目的Build文件中加入web.config文件。文件内写入:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <system.webServer>
            <staticContent>
                    <remove fileExtension=".unityweb" />
                    <mimeMap fileExtension=".unityweb" mimeType="application/octet-stream" />
            </staticContent>
            <rewrite>
                    <outboundRules>
                        <rule name="Append gzip Content-Encoding header">
                            <match serverVariable="RESPONSE_Content-Encoding" pattern=".*" />
                            <conditions>
                                    <add input="{REQUEST_FILENAME}" pattern="\.unityweb$" />
                            </conditions>
                            <action type="Rewrite" value="gzip" />
                        </rule>
                    </outboundRules>
            </rewrite>
    </system.webServer>
</configuration>
```  
具体文章: [WebGL: Deploying compressed builds](https://www.jianshu.com/p/609c85e96440)