![Разница между управляемыми (controlled) и не управляемыми (uncontrolled) компонентами?](https://youtu.be/yvOXvZ8aEFo?t=684)

![](https://www.youtube.com/watch?v=oqD42QsW2vU&t=2s)
#### Ответ

![[Pasted image 20230704174628.png|600]]

Одна из основных идей React, это наличие контроля над компонентами и управление их собственным состоянием. Что случится если мы отправим чистый HTML элементов формы (input, select, textarea и т.д.) в общей куче? Должны ли мы иметь React, как “единственный источник правды” или мы должны позволить, чтобы данные формы существовали в DOM в HTML-форме? Эти два вопроса лежат в основе **контролируемых (controlled)** и **неконтролируемых** (**uncontrolled)** компонентов.

##### Контролируемый компонент

**Контролируемый компонент**— это такой компонент, где React осуществляет контроль и является единственным источником правды для данных формы. Как вы можете видеть ниже, _username_ существует не в DOM, а нашем состоянии компонента. Всякий раз, когда хотим обновить _username_, мы вызываем _setState,_ как мы уже привыкли.

```jsx
class ControlledForm extends Component {  
  state = {  
    username: ''  
  }  
  updateUsername = (e) => {  
    this.setState({  
      username: e.target.value,  
    })  
  }  
  handleSubmit = () => {}  
  render () {  
    return (  
      <form onSubmit={this.handleSubmit}>  
        <input  
          type='text'  
          value={this.state.username}  
          onChange={this.updateUsername} />  
        <button type='submit'>Submit</button>  
      </form>  
    )  
  }  
}
```

##### Неконтролируемый компонент

**Неконтролируемый компонент** — это такой компонент, где ваши данные формы обрабатываются в DOM, а не внутри вашего компонента.

```jsx
class UnControlledForm extends Component {  
  handleSubmit = () => {  
    console.log("Input Value: ", this.input.value)  
  }  
  render () {  
    return (  
      <form onSubmit={this.handleSubmit}>  
        <input  
          type='text'  
          ref={(input) => this.input = input} />  
        <button type='submit'>Submit</button>  
      </form>  
    )  
  }  
}
```

##### Разница между управляемым и неуправляемым компонентом?

*Управляемые компонент принимает своё текущее значение в качестве пропсов, а также коллбек для изменения этого значения.*

Хотя неконтролируемые компоненты обычно проще в реализации, так как вы просто берете значение из DOM используя refs, *рекомендуется использовать контролируемые компоненты. Основная причина этого в том, что контролируемые компоненты поддерживают мгновенную проверку полей, позволяют вам условно отключать/включать кнопки, устанавливать формат входных данных и, вообще, более отражают суть React.*

![[Pasted image 20230912152217.png|600]]

Подробнее: [Контролируемый и неконтролируемый компонент](https://habr.com/ru/post/502034/)

____
#React #controlled #uncontrolled

____

#### [[004 React + Redux|Назад]]