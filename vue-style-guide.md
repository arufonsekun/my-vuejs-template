## Sumarização dos padrões de desenvolvimento do VueJS
Cada padrão se encontra dentro de uma categoria: Essencial, Fortemente Recomendado, Recomedado e Use com cuidado.

### Padrões Essenciais

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
 e referências privadas do VueJS serem prefixadas com `_`, desse modo a melhor maneira de nomear propriedades
 privadas definidas pelo usuário é unindo os dois prefixos.

### Fortemente Recomendados

1. **Arquivos de componentes** são fortemente recomendados, uma vez tendo os componentes
definidos em arquivo específicos torna-se mais rápido de encontrá-los, e revisá-los.


**Fonte**: [VueJS Style Guides](https://vuejs.org/v2/style-guide)
