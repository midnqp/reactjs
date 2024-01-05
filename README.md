## introduction
react is a library to write reusable components. it's not a framework, angular is a framework as that covers more ground. 
a huge part of react is on top of JSX, javascript xml. it's an extension of javascript that lets us write html-like code within javascript.

```jsx
export default function App() {
  return <p>Hello, World!</>
}
```

## component

a react component is a reusable block of UI that renders JSX markup based on props and state.
```jsx
function Card(props) {
  return (<div className='Card'>
    <h1>{props.title}</h1>
    <p>{props.text}</p>
  </div>)
}
```

a component function cannot be async:
```jsx
async function getNotesData() {
  const dataList = await (await fetch('/notes.json')).json()
  return dataList
}

function CardList() {
  const [dataList, setDataList] = useState([])

  useEffect(() => {
    getNotesData().then(dataList => setDataList(dataList))
  }, [])

  return dataList.map(data => <Card title={data.title} text={data.text} />)
}
```

a component can have children:
```jsx
function ImageCard(props) {
  return (
    <>
      <img src={props.imageUrl}/>
      {props.children}          
    </>    
  )
}

function Caption(props) {
  return <p>{props.text}</p>
}

export default function ImageViewer() {
  return (
    <ImageCard imageUrl='https://i.imgur.com/YfeOqp2s.jpg'>
      <Caption text='caption of an image' />    
    </ImageCard>
  )
}
```