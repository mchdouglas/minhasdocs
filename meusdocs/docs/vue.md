## Iniciando com vue js
* `console.log('estudando vue.js')`
## O que é vue.js?
Um framework progressivo para a construção de interfaces de usuário.
 
## Renderização Declarativa
No núcleo do Vue.js está um sistema que nos permite declarativamente renderizar dados no DOM (Document Object Model) usando uma sintaxe de template simples.

## Símbolo de eventos no vue
O símbolo de eventos no vue é o *`@`* .

## O que é um componente no vue.js?
Componentes são instâncias reutilizáveis do Vue com um nome.
É um arquivo com marcação de texto, estilo e scripts. 

## Comunicação através de propriedades (`props`)
Para podermos passar dados a partir de um componente pai, o componente filho deve declarar explicitamente oque é esperado.

## Passando dados para o componente pai (`emissão`)
Como no Vue o fluxo de dados é unilateral e as propriedades não podem ser passadas para o componente pai. Então podemos usufruir do sistemas de eventos personalizados do Vue, para podermos emitir eventos para o componente pai através do `$emit`, assim subindo níveis e podendo passar dados.

## O que é um bind em vue
Serve para ligar a um atributo (pode ser `v-bind` ou `:`).