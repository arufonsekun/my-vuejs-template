## Sumarização dos padrões de desenvolvimento do VueJS

### Lista de tópicos
Cada padrão encontra-se em uma categoria, são eles: 
1. [Essenciais](#essenciais) cuja intenção é previnir erros.
2. [Fortemente recomendados]() são padrões que objetivam melhorar a legibilidade do código.
3. [Recomendados]() que buscam minimizar escolhar arbitrárias e discuções desnecessárias.
4. [Usar com cuidado]() apontado pela documentação como padrões com "perigo em potencial".

### Essenciais

1. O **nome de componentes** deve ser formado por várias palavras. Ex: TodoItem.
2. A **definição das props** deve ser a mais detalhada possível, ao menos
o tipo deve ser especificado. Props devidamente descritas tornam o entendimento
do componente mais simples. Ex:

     ```javascript
     props: {
         status: {
             type: String,
             required: true,
             validator: function(){...}
         }
     }
     ```
3. **Evite** declarações `v-if` no mesmo elemento juntamente com declarações `v-for`. 
No exemplo a seguir, toda vez em que é necessário re-renderizar os elementos toda
a lista de usuários é percorrida.

     ```html
     <ul>
         <li
             v-for="user in users"
             v-if="user.active"
             :key="user.id"
         >
             {{ user.name }}
         </li>
     </ul>
     ```

     Processamento desnecessário que pode ser evitado criando uma _computed property_.      
     
     ```javascript
     computed: {
         activeUsers(){
             this.users.filter(function(user){
                 return user.active;
             }); 
         }
     }
     ```
4. O **escopo dos estilos** dos componentes deve ser restrito, com exceção dos estilos
do componente raiz ─ App ─ e de componentes de layout.

    ```html
    <style scoped>
        .btn {
            color: #eee;
            font-size: 1rem;
        }
    </style>
    ```
5. O **nome de propriedades privadas** em plugins, mixins e componentes deve conter o prefixo
`$_`. Isso foi esquematizado devido as referências com o prefixo `$` serem recursos públicos do framework,
 e referências privadas serem prefixadas com `_`, desse modo a melhor maneira de nomear propriedades
 privadas definidas pelo usuário definida foi unir os dois prefixos, fazendo isso não há chances de ocorrer
 algum tipo de problema com referências.

### Fortemente Recomendados

1. Criar **arquivos de componentes** é uma prática bastante interessante, uma vez tendo os componentes
definidos em arquivos específicos torna-se mais fácil encontrá-los, e revisá-los. Esse padrão é bastante 
conveniente quando analisando-o da perspectiva de projetos bastante extensos.

2. **Nome de arquivo de componente** deve ser sempre PascalCase ou kebab-case.

**Fonte**: [VueJS Style Guides](https://vuejs.org/v2/style-guide)
