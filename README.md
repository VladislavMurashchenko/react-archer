# react-archer
This is a small extension for
[![CircleCI](https://circleci.com/gh/pierpo/react-archer.svg?style=svg)](https://circleci.com/gh/pierpo/react-archer)

🏹 Draw arrows between DOM elements in React 🖋

## Installation

`npm install react-archer --save` or `yarn add react-archer`

## Example

[Try it out!](https://pierpo.github.io/react-archer/)

![Example](https://raw.githubusercontent.com/pierpo/react-archer/master/example.png)

```jsx
import { ArcherContainer, ArcherElement } from 'react-archer';

const rootStyle = { display: 'flex', justifyContent: 'center' };
const rowStyle = { margin: '200px 0', display: 'flex', justifyContent: 'space-between', }
const boxStyle = { padding: '10px', border: '1px solid black', };

const App = () => {
  return (
    <div>

      <ArcherContainer strokeColor='red' >
        <div style={rootStyle}>
          <ArcherElement
            id="root"
            relations={[{
              targetId: 'element2',
              targetAnchor: 'top',
              sourceAnchor: 'bottom',
            }]}
          >
            <div style={boxStyle}>Root</div>
          </ArcherElement>
        </div>

        <div style={rowStyle}>
          <ArcherElement
            id="element2"
            relations={[{
              targetId: 'element3',
              targetAnchor: 'left',
              sourceAnchor: 'right',
              style: { strokeColor: 'blue', strokeWidth: 1 },
              label: <div style={{ marginTop: '-20px' }}>Arrow 2</div>,
            }]}
          >
            <div style={boxStyle}>Element 2</div>
          </ArcherElement>

          <ArcherElement id="element3">
            <div style={boxStyle}>Element 3</div>
          </ArcherElement>

          <ArcherElement
            id="element4"
            relations={[{
              targetId: 'root',
              targetAnchor: 'right',
              sourceAnchor: 'left',
              label: 'Arrow 3',
            }]}
          >
            <div style={boxStyle}>Element 4</div>
          </ArcherElement>
        </div>
      </ArcherContainer>

    </div>
  );
}

export default App;
```

## API

### `ArcherContainer`

| Name | Type | Description |
| - | - | - |
| `strokeColor` | `string` | A color string `'#ff0000'`
| `strokeWidth` | `number` | A size in `px`
| `arrowLength` | `number` | A size in `px`
| `arrowThickness` | `number` | A size in `px`
| `children` | `React.Node` |

### `ArcherElement`

| Name | Type | Description |
| - | - | - |
| `id` | `string` | The id that will identify the Archer Element. Should only contain alphanumeric characters and standard characters that you can find in HTML ids.
| `children` | `React.Node` |
| `relations` | `Array<Relation>` |

The `Relation` type has the following shape:

```javascript
{
  targetId: string,
  targetAnchor: 'top' | 'bottom' | 'left' | 'right',
  sourceAnchor: 'top' | 'bottom' | 'left' | 'right',
  label: React.Node,
  style: Style,
}
```

The `Style` type has the following shape:

```javascript
{
  strokeColor: string,
  strokeWidth: number,
  arrowLength: number,
  arrowThickness: number
}
```

## TODO

- Automatic anchoring option
- Options to customize the path shape more (straight line, right angle line, smoothed right angle path)
- Add a Code Sandbox
