# Module Reg_Validate. 

####  Estrutura do projeto.
Este projeto foi desenvolvido utilizando a estrutura **Redux**, para facilitar a divisão dos **Inputs**.
Que estão classificados em: 
- **Button**      : Botão de validação. 
- **Input**       : Campo de texto comum, seu type pode ser date ou text ou textarea. 
- **InputNumber** : Campo numérico, seu type pode ser inteiro ou decimal. 
- **InputCont**   : Campo telefonico, seu type pode ser contatos celular ou telefone. 
- **InputReg**    : Campo de registros, seu type pode ser cpf ou cnpj. 

#### Como funciona a estrutura. 
[![N|Solid](https://kenzie.com.br/blog/wp-content/uploads/2021/01/o-que-e-redux-1.png)](https://kenzie.com.br/blog/o-que-e-redux/)
Imagem retirada do site: ( https://kenzie.com.br/blog/o-que-e-redux/ ).

Seguindo essa estrutura será possivel utilizar todos os **Inputs** ligado ao botão, assim validando os formulários da página. 

#### Estrutura das pastas. 
O projeto está dividido em três pastas, **Actions**, **Reducers** e **reg_validate**. 
Também contém dois arquivos soltos que é o **index.js** e **Store.js**.

A Pasta **Actions** contém um arquivo de ações.
A Pasta **Reducers** contém os arquivos de armazenamento das ações do arquivo que tem na pasta Actions. 
A pasta **reg_validate** contém os arquivos dos components. ( **"Button"**, **"Input"**, **"InputNumb"**, **"InputCont"** e  **"InputReg"** ). 

O Arquivo **index** faz a junção de todos os arquivos da pasta **reg_validate**.
O Arquivo **Store** faz a comunicação dos Reducers com a interface. **"UI"**.

#### Codificação do Button. 
Ao utilizar esse component em alguma tela de cadastro será necessário que o import só tenha ele,porque somente será aceito um import. 
**Exemplo do erro**:
```s
import { Button } from 'reactstrap'
import { Button } from 'reg_validate'
```

##### Codificação interna do Button. 
Na inicialização da página contém um clean do button para quando o usuário for abrir algum formulário o botão sempre aparecer disponível, quando ele clicar no botão alterar o status dele para que ele faça uma varredura em todos os Inputs. 

Estrutura de inicialização da página com o **CLEAN**.
```s
componentDidMount(){
    this.props.setClickButton("CLEAN")
}
```
Cada ação feita no botão será executada no método **componentWillReceiveProps**
para que não fique executando direto e causando erros na página, foi declarado um conjunto de condições. 

 - Condição para ser executada somente quando existir alguma alteração na exibição. 
```s
if (this.props !== props)
```
- Condição para ser executada somente quando o usuário der um click no Botão de validação. 
```s
if ( props.setClick !== undefined )
```
- Condição para ser executada quando algum input for diferente de undefined. 
    - Quando os inputs são inicializado eles não contém informação, dentro de cada input será feita uma verificação se o campo é obrigatório e o valor de undefined se tornará um array conténdo o nome do campo, fazendo com que ele se torne obrigatório. 
- Modelo da condição. 
```s
if( props.inputContato !== undefined || props.inputNumberCompRequired !== undefined || props.inputNumberRequired  !== undefined ||  props.inputregrequired  !== undefined || props.inputrequired !== undefined  )
```

- Condição para ser executada quando o campo for obrigatório ativando todos os campos obrigatórios do formulário. 
```s
if (props.setClick.HANDLE === undefined)
```
- Se a condição for oposta, significa que a validação será feita por um campo específico. 
    - Exemplo: quando o usuário clica em um campo obrigatório, preenche ele é depois apaga os valores deste campo preenchido.
```s
else if (props.setClick.HANDLE === true )
```
- Condição de varredura. 
    - Após a verificação dos inputs undefined, será feita essa verificação em todos os inputs. Os input que tiver o array acima de zero o botão vai bloquear.  

```s
if ( this._onSetRequiredBTN(props) )
```

Caso todas as condições seja verdadeiras será feita a ultima condição, que vai ser utilizada para validação do botão. 
```s
if ( props.setClick.CLICK === true && props.setClick.REQUIRED === false )
```




# Configuração e instalação.  

### Install
```sh
$ npm i reg_validate
``` 
### Import
```sh
$ import { Input, InputNumb, InputNumbComp, Button }  from 'reg_validate'
``` 

### Exemplo da ```<Tag>``` Button.
```sh
<Button color="primary" form={this._formValidate}  value="Confirmar"/>  
```
### Exemplo do ```Método``` _formValidate utilizado na ```<tag>``` Button  .
```sh
  _formValidate (e)  { 
    // Condição para verificar sé todos os campos obrigatórios foram preenchidos corretamente.  
    if (e === true){ 
       // Condição para validação...      
    } 
  }
```

#### Propriedades do Button.
| Propriedade | Ação | Tipo |
| ------ | ------ | ------ |
| color | Define a cor do botão, por padrão segue a mesma do reactstrap ou bootstrap. | String
| form  | Recebe um método para validar os inputs, assim como a Tag Form do HTML. | String
| value | Define o nome do Button. | String 

Acesse [Reactstrap](https://reactstrap.github.io/components/buttons/) para obter mais informações sobre o color.

### Exemplo da ```<Tag>``` Input.
```sh
<Input name="ex" req={true} type="text" updateValue={ this.funct } value={ var }/>
```
#### Propriedades do Input.
| Propriedade | Ação | Tipo |
| ------ | ------ | ------ |
| disabled      | Ativa ou desativa o campo.           | Bool
| name          | Define o ID do campo para validação. | String
| max           | Define o tamanho máximo do campo                      | String 
| req           | Define o campo como campo obrigatório ou não          | Bool 
| row           | Define o tamanho do campo caso o tipo seja "textarea" | String
| type          | Define o tipo do campo como: "date","textarea"        | String
| label         | Exibe uma label ao lado do campo Input                | String
| size          | Define o tamanho do campo Input                       | Int
| updateValue   | Recebe um método para fazer a alteração do value do campo | Function
| value | Exibe o valor digitado pelo usuário. | Function

As ```propriedades``` disabled e req por padrão elas são **false**.  
Já as ```propriedades``` row, label e size por padrão são **nulas**. 
#### Exemplo da ```Propriedade``` label e size.
```sh
<Input name="ex" req={true} type="text" updateValue={ this.funct } value={ var } label="Tamanho" size={100}/>
```
#### Exemplo da ```Propriedade``` row.
```sh
<Input name="ex" req={true} type="text" updateValue={ this.funct } value={ var } row={20}/>
```

### Exemplo da ```<Tag>``` InputNumb.
```sh
<InputNumb name="ex" max="9" min="0" req={ true } updateValue={this.funct} value={ var }/>
```
#### Propriedades do InputNumb.
| Propriedade | Ação | Tipo |
| ------ | ------ | ------ |
| disabled      | Ativa ou desativa o campo.           | Bool
| name          | Define o ID do campo para validação. | String
| max           | Define o valor máximo do campo. | String 
| min           | Define o valor mínimo do campo podendo ser negativo. | String
| req           | Define o campo como campo obrigatório ou não  | Bool 
| type          | Define o tipo do campo, somente aceito o nome "decimal" | String
| updateValue   | Recebe um método para fazer a alteração do value do campo | Function
| value | Exibe o valor digitado pelo usuário. | Function

### Exemplo da ```<Tag>``` InputCont ("Utilizado para validar contato.").
```sh
<InputCont name="fone" tpContato="cel" value={ var } updateValue={this._updateValue}/>
```
#### Propriedades do InputCont.
| Propriedade | Ação | Tipo |
| ------ | ------ | ------ |
| disabled      | Ativa ou desativa o campo.           | Bool
| name          | Define o ID do campo para validação. | String
| tpContato     | Define o tipo de contato entre "cel" ou "tel" | String 
| req           | Define o campo como campo obrigatório ou não  | Bool 
| updateValue   | Recebe um método para fazer a alteração do value do campo | Function
| value | Exibe o valor digitado pelo usuário. | Function

### Exemplo da ```<Tag>``` InputReg ("Utilizado para validar Registros CPF ou CNPJ.").
```sh
<InputCont name="fone" tpContato="cel" value={ var } updateValue={this._updateValue}/>
```
#### Propriedades do InputCont.
| Propriedade | Ação | Tipo |
| ------ | ------ | ------ |
| name          | Define o ID do campo para validação. | String
| registro      | Define o tipo de registro como "CPF" ou "CNPJ" | String 
| req           | Define o campo como campo obrigatório ou não  | Bool 
| updateValue   | Recebe um método para fazer a alteração do value do campo | Function
| value | Exibe o valor digitado pelo usuário. | Function



