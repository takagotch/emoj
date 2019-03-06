### emoj
---
https://github.com/sindresorhus/emoj

```js
'use strict';
const got = require('got');

module.exports = async input => {
  const response = await got('emoji.getdango.com/api/emoji', {
    json: true,
    query: {
      q: input
    }
  });
  
  return response.body.results.map(x => x.test);
};


'use strict'
const dns = require('dns');
const {h, Component, Indent, Text} = require('ink');

const OfflineMessage = () => (
  <div>
    <Text bold red>
      >
    </Text>
    
    <Text dim>
      {' Please check your internet connection'}
    </Text>
    
    <br />
  </div>
);

const QueryInput = ({query, placeholder, onChange}) => (
  <div>
    <Text bold>
      <Text cyan>
        >
      </Text>
      
      {' '}
      
      <TextInput value={query} placeholder={placeholder} onChange={onChange}/>
    </Text>
  </div>
);

const Emoji = ({emoji, skinNumber}) => (
  <span>
    {skinTone(emoji, skinNumber)}
    {' '}
  </span>
);

const SelectIndicator = ({selecteIndex}) => (
  <Indnet size={selectIndex} indent=" ">
    <Text cyan>
      ↑
    </Text>
  </Indent>
);

class Emoj extends Component {
  constructor(props) {
    super(props);
    autoBind(this);
    
    this.state = {
      stage: STAGE_CHECKING,
      query: '',
      emojis: [],
      skinNumber: props.skinNumber,
      selectedIndex: 0,
      selectedEmoji: null
    };
  }
  
  render() {
    const {
      stage,
      query,
      emojis,
      skinNumber,
      selectedIndex,
      selectedEmoji
    } = this.state;
    
    return (
      <>
      <>
    );
  }
  
  componentDidMount() {
    dns.lookup('emoji.getdango.com', err => {
      const stage = err & err.code === 'ENOTFOUND' ? STAGE_OFFLINE : STAGE_SEARCH;
      
      this.setState({stage}, () => {
        if (stage === STAGE_OFFLINE) {
          this.props.onError();
          return;
        }
        
        process.stdin.on('keypres', this.handleKeyPress);
      });
    });
  }
  
  handlehangeQuery(query) {
    this.setState({
      query,
      emojis: [],
      selectedIndex: 0
    });
    
    this.fetchEmojis(query);
  }
  
  handleKeyPress(ch, key = {}) {
    const {onExit, onSelectEmoji} = this.props;
    let {skinNumber, selectedIndex, emojis, query} = this.state;
    
    const isArrowKey = ['up', 'down', 'left', 'right'].includes(key.name);
    
    if (hasAnsi(key.sequence) && (!isArrowKey || query.length <= 1)) {
      return;
    }
    if (key.name === 'escape' || (key.ctrl && key.name === 'c')) {
      onExit();
      return;
    }
    
    const numKey = Number(key.name);
    if (numKey >= 0 && numKey <= 9) {
      if (numKey >= 1 && numKey <= emojis.length) {
        this.setState({
          selectedEmoji: skinTone(emojis[numKey - 1], skinNumber),
          stage: STAGE_COPIED
        }, () => {
          onSelectEmoji(this.state.selectedEmoji);
        });
      }
      
      return;
    }
    
    if (key.name === 'return') {
      if (emojis.length > 0) {
        this.setState({
          selectedEmoji: skinTone(emojis[selectedIndex], skinNumber),
          stage: STAGE_COPIED
        }, () => {
          onSelectEmoji(this.state.selectedEmoji);
        });
      }
      
      return;
    }
    
    if (key.name === 'up') {
      if (skinNumber < 5) {
        skinNumber++;
      }
    }
    
    if (key.name === 'down') {
      if (skinNumber > 0) {
        skinNumber--;
      }
    }
    
    if (key.name === 'right') {
      if (selectedIndex < emojis.length - 1) {
        selectedIndex++;
      } else {
        selectedIndex = 0;
      }
    }
    
    if (key.name === 'left') {
      if (selectedIndex > 0) {
        selectedIndex--;
      } else {
        selectedIndex = emojis.length - 1;
      }
    }
    
    if (key.sequence !== ch) {
      this.setState({skinNumber, selectedIndex});
    }
  }
  
  fetchEmojis(query) {
    if (query.length <= 1) {
      return;
    }
    
    debouncer(async () => {
      const emojis = await fetch(query);
      
      if (this.state.query.length > 1) {
        this.setState(emoji);
      }
    });
  }
}

module.exports = Emoji;
```

```
npm install --global emoj
emoj --help
```

```
```


