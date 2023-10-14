#### Ответ

*Презентационные компоненты обычно отвечают за отрисовку элементов пользовательского интерфейса на экране.* Они получают данные и обратные вызовы в качестве пропсов. Обычно они сосредоточены на рендеринге JSX и не знают о состоянии или действиях приложения. 

Вот пример презентационного компонента:

```javascript
import React from 'react';

function Button(props) {
  return <button>{props.label}</button>;
}
```

*Компоненты-контейнеры обычно отвечают за управление состоянием и действиями.* Они содержат логику для выборки данных, обработки пользовательского ввода и выполнения других задач. Они знают о состоянии и действиях приложения и передают данные и обратные вызовы презентационным компонентам через пропсы. 
Вот пример компонента-контейнера:

```javascript
import React, { Component } from 'react';
import Button from './Button';

class Form extends Component {
 state = {
   name: '',
 };

 handleChange = (event) => {
   this.setState({ name: event.target.value });
 };

 handleSubmit = (event) => {
   event.preventDefault();
   // отправка формы
 };

 render() {
   return (
     <form onSubmit={this.handleSubmit}>
       <label>
         Name:
         <input type="text" value={this.state.name} onChange={this.handleChange} />
       </label>
       <Button label="Submit" />
     </form>
   );
 }
}
```

*Разделение презентационных и контейнерных компонентов может помочь упростить понимание, тестирование и поддержку вашего кода за счет отделения задач, связанных с тем, как вещи выглядят, от того, как они работают.*

____
#React #presentation #container 

____

#### [[004 React + Redux|Назад]]