## Axios no VueJs
* `vue add axios` - Para adicionar ao seu projeto vue.

<p>
 Agora iremos fazer uma breve configuração para não ficarmos repetindo a url de requisição. Para isso você irá criar um arquivo chamado  <code>.env.local</code> e dentro do arquivo irá escrever os seguintes comandos:       
<code>VUE_APP_BASE_URL=http://sua-url-de-requisição</code>.
<p>Depois dentro do arquivo de configuração colar o seguinte código:
<pre><code>let config = {
    baseURL: process.env.VUE_APP_BASE_URL
}</code></pre>
</p>