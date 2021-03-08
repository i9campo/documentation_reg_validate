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
