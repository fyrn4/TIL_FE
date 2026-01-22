```jsx
# App.jsx 

const element1 = <h1> hello <h1/> /* 이처럼 태그형태도 변수로 지정 가능 */
const element2 = (
  <ul>
    <li>A</li>
    <li>B</li>
    <li>C</li>
  </ul>
)

function App(){
  return (
    <>
      {/* JSX 주석 */}
      {element1}
      <BasicExpressions />
    </>
  )
}

function BasicExpressions() {
  const name = "John";
  const age = 21;
  const isAdmin = true;

  return (
    <div>
      <p>Name: {name}</p>
      <p>Age: {age+1}</p>
      <p>{name+"'s Profile"}</p>
      <p>{`${name} is ${age} years old`}</p>
      <p>Admin Status: {String(isAmdin)}</p>
    </div>
  )
}
export default App
