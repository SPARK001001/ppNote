CSP（Content Security Policy）是一种用于增强网页安全性的安全策略，它通过限制浏览器加载和执行资源的来源来减少跨站点脚本攻击（XSS）、数据盗取等安全风险。CSP的核心思想是告诉浏览器哪些内容是被允许加载的，从而减少恶意内容的影响。

CSP通过在HTTP头部的`Content-Security-Policy`字段中设置策略规则来实现。这些策略规则可以限制页面内的内容来源、脚本执行方式、样式加载等。以下是一些常见的CSP策略规则：

- `default-src`：设置默认的内容来源，如果没有明确的规则匹配，将使用默认的策略。
- `script-src`：指定可以执行脚本的来源，用于防止XSS攻击。
- `style-src`：指定可以加载样式的来源，用于防止CSS注入攻击。
- `img-src`：指定可以加载图片的来源，用于防止图片注入攻击。
- `font-src`：指定可以加载字体的来源。
- `frame-src`：指定可以加载框架的来源，用于防止点击劫持等攻击。
- `connect-src`：指定可以与后端进行通信的来源，用于限制数据泄露。
- `media-src`：指定可以加载媒体资源的来源。
- `object-src`：指定可以加载嵌入对象的来源。

通过设置这些策略规则，网站可以限制浏览器只加载来自可信任源的内容，防止恶意脚本的执行，从而增强网页的安全性。同时，CSP还可以通过报告机制来监控违反策略的行为，帮助网站管理员及时检测和应对安全问题。

需要注意的是，CSP的配置需要经过充分的测试和验证，因为过于严格的策略可能会影响网站的正常功能。不同的网站根据自身情况可以定制不同的CSP策略规则来平衡安全性和功能需求。