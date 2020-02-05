#  React

```js
#App.js

import React, { Component } from 'react';
import PhoneForm from './components/phone_form';
import PhoneList from './components/phone_list';

class App extends Component {
  id = 1;
  state = {
    contacts: [
      {
        id: 0,
        name: '관리자',
        phone: '010-1234-5678'
      }
    ]
  }

  handleCreate = (data) => {
    //console.log(data);
    //data -> contact 배열에 추가

    const { contacts } = this.state;

    //console.log(this.state);
    //console.log(this.state.contacts);
    //console.log(contacts);

    this.setState({
      contacts: contacts.concat({ id: this.id++, ...data })
    })
  }

  handleRemove = (selected_id) => {
    // state의 contacts에서 해당 ID값을 삭제
    const { contacts } = this.state;

    this.setState({
      contacts: contacts.filter(
        info => info.id !== selected_id
      )
    });
  }

  handleUpdate = (selected_id, data) => {
    const { contacts } = this.state;
    //this.state
    console.log('selected_id =' + selected_id)
    this.setState({
      contacts: contacts.map(
        item => item.id === selected_id
          ? { ...item, ...data } // 데이터 수정
          : item //기존데이터 유지

      )
    });
  }

  render() {
    const { contacts } = this.state
    return (
      <div>
        <PhoneForm
          onCreate={this.handleCreate} />

        <PhoneList
          data={this.state.contacts}
          onRemove={this.handleRemove}
          onUpdate={this.handleUpdate} />
      </div>
    );
  }
}

export default App;
```



```js
#phone_form

import React, { Component } from 'react';

class PhoneForm extends Component {
    state = {
        name: '',
        phone: ''
    };

    handleChange = (e) => {
        //console.log(e.target.value);
        this.setState({
            [e.target.name]: e.target.value
        })
    }

    handleSubmit = (e) => {
        e.preventDefault();
        this.props.onCreate(this.state);
        this.setState({
            name: '',
            phone: ''
        })
    }

    render() {
        return (
            <form onSubmit={this.handleSubmit}>
                <input
                    value={this.state.name}
                    placeholder='이름을 입력하세요'
                    onChange={this.handleChange}
                    name='name' />
                <input
                    value={this.state.phone}
                    placeholder='전화번호를 입력하세요'
                    onChange={this.handleChange}
                    name='phone' />
                <button type="submit">
                    등록
                </button>
            </form>
        );
    }
}

export default PhoneForm;
```



```js
#phone_list

import React, { Component } from 'react';
import PhoneItem from './phone_item';


class PhoneList extends Component {
    render() {
        const { data, onRemove, onUpdate } = this.props; //data -> contacts
        //const data = this.props; //contacts -> data.contacts

        const list = data.map(value => (  //for문장과 동일
            <PhoneItem 
            key={value.id} // key값을 설정
            info={value}
            onRemove={onRemove}
            onUpdate={onUpdate}/>
            ) 
        );
        return (
            <div>
                {list}
            </div>
        );
    }
}

export default PhoneList;
```



```js
#phone_item

import React, { Component } from 'react';


class PhoneItem extends Component {

    state = {
        editable: false,
        name: '',
        phone: ''
    }

    componentDidUpdate(preProps, prevState) {
        const { info, onUpdate } = this.props;
        console.log(info.name + "/" + info.phone);
        console.log(onUpdate);
        console.log(prevState.editable + "/" + this.state.editable);

        if (!prevState.editable && this.state.editable) {
            this.setState({
                name: info.name,
                phone: info.phone
            })
        }

        // update
        if (prevState.editable && !this.state.editable) {
            onUpdate(info.id, { name: this.state.name, phone: this.state.phone });
        }
    }

    handleRemove = (e) => {
        const { info, onRemove } = this.props;
        onRemove(info.id);
    }

    handleUpdate = (e) => {
        const { editable } = this.state;
        this.setState({
            editable: !editable
        });
    }

    handleChange = (e) => {
        const { name, value } = e.target;
        this.setState({
            [name]: value
        });
    }

    render() {
        const css = {
            border: '1px solid black',
            padding: '8px',
            margin: '5px'
        };

        const { editable } = this.state;
        if (editable) {
            console.log('수정모드');
            return (
                <div style={css}>
                    <div>
                        <input value={this.state.name}
                            name="name"
                            placeholder="이름을 입력하세요"
                            onChange={this.handleChange} />
                    </div>
                    <div>
                        <input value={this.state.phone}
                            name="phone"
                            placeholder="전화번호를 입력하세요"
                            onChange={this.handleChange} />
                    </div>
                    <button onClick={this.handleRemove}>삭제</button>
                    <button onClick={this.handleUpdate}>적용</button>
                </div>
            );
        }
        else {
            console.log('일반모드');
        }

        //const info = this.props.info;
        //console.log(info.id);
        //console.log(info.name);
        //console.log(info.phone);

        const { name, phone, id } = this.props.info; //위의 방식과 동일한 방식 -> 동일한 결과
        //console.log(id);
        //console.log(name);
        //console.log(phone);

        return (
            <div style={css}>
                <div><b>{name}</b></div>
                <div><b>{phone}</b></div>
                <button onClick={this.handleRemove}>삭제</button>
                <button onClick={this.handleUpdate}>수정</button>
            </div>
        );
    }
}

export default PhoneItem;
```

