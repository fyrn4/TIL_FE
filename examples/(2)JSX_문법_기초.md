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

function ObjectArrayExpressions() {
  const user = {
    name: "Jane",
    email: "jane@example.com"
  }
  const colors = ["red","blue","green"]
  const numbers = [1,2,3,4,5]

  return (
    <div>
      <p>User: {user.name}</p>
      <p>first color: {colors[0]}</p>
      <p>Color count: {colors.length}</p>
      <p>Doubleds: {
        numbers.map(n => n*2).join(", ")
      }</p>
      <p> Evens : {numbers.filter(n=>n%2 ===0).join(", ")} </p>
    </div>
  )
}

function FunctionExpressions() {
  const getGreeting = (name) => `Hello, ${name}!`;
  const formatDate = (date) => {
    return new Date(date).toLocaleDateString();
  }
  const calculateTotal = (items) => {
    return items.reduce((sum, item) => sum + item.price, 0);
    /*
      array.reduce((누적값, 현재값) => {
        return 새로운_누적값;
      }, 초기값);
     */
  }
  const itemArr = [{id:1, price:10}, {id:2, price:20}];

  return (
    <div>
      <p>{getGreeting("Alice")}</p>
      <p>Today : {formatDate(new Date())}</p>
      <p>Total: ${calculateTotal(itemArr)}</p>
      <p>Good {(()=> {
        const hours = new Date().getHours();
        return hours < 12 ? "Morning" : "Afternoon";
      })()}</p>
      /* Good 부분 즉시실행함수 설명
      <p>Good {여기에 JS 식 사용가능}</p>
      핵심 포인트(함수를 정의하자마자 사용) : (() => { ... })()
        (function () {
          const hours = new Date().getHours();
          return hours < 12 ? "Morning" : "Afternoon";
        })();
      위와 같다.
      추가로, { if (hours < 12) { ... } } 이와같이 즉시실행함수 jsx 안에서는 if문을 직접 쓸수가없다.
      */
    </div>
  )
}


export default App
