<h3>예제1</h3>

```css
# Card.module.css
.card {
  width: 224px;
  margin: 12px auto;
  padding: 24px;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.card h2 {
  margin: 0 0 8px;
  font-size: 1.33rem;
  color: #333;
}

.card p {
  margin: 2px 0;
}

.card p:last-child {
  font-size: 0.92rem;
  color: #888;
}
```
```jsx
# InfoCard.jsx
import styles from './Card.module.css'

const InfoCard = (props) => (
  <div className={styles.card}>
    <h2>{props.title}</h2>
    <p>{props.content}</p>
    <p>Author: {props.author}</p>
  </div>
)

/* 아래는 props의 직접명시(디스트럭처링) 가능 */
const InfoCard = ({ title, content, author }) => (
  <div className={styles.card}>
    <h2>{title}</h2>
    <p>{content}</p>
    <p>Author: {author}</p>
  </div>
)

/* 아래는 디스트럭처링 된 객체에 기본값을 지정 가능 */
const InfoCard = ({ 
  title="(No Title)",
  content,
  author="Anonymous" 
}) => (
  <div className={styles.card}>
    <h2>{title}</h2>
    <p>{content}</p>
    <p>Author: {author}</p>
  </div>
)

export default InfoCard
```
```jsx
# App.jsx (1번 형태)
import InfoCard from './InfoCard'

function App() {

  return (
    <>
      <InfoCard 
        title="Props in React"
        content="Props pass data from one component to another."
        author="Alice"
      />
      <InfoCard 
        title="React Composition"
        content="Composition makes your components more reusable"
        author="Charlie"
      />
    </>
  )
}

export default App

# App.jsx (2번 형태)
import InfoCard from './InfoCard'

const cardData1 = {
  title: "Props in React",
  content: "Props pass data from one component to another.",
  author: "Alice"
};
const cardData2 = {
  title: "React Composition",
  content: "Composition makes your components more reusable"
};

function App() {

  return (
    <>
      <InfoCard {...cardData1} />
      <InfoCard {...cardData2} />
    </>
  )
}
export default App

# App.jsx (3번 형태)
import InfoCard from './InfoCard'

const cards = [
  {
    idx: 1,
    title: "Props in React",
    content: "Props pass data from one component to another.",
    author: "Alice"
  }, {
    idx: 2,
    title: "React Composition",
    content: "Composition makes your components more reusable"
  }
]

function App() {

  return (
    <>
      {cards.map(cardData => (
        <InfoCard key={cardData.idx} {...cardData} />
      ))}
    </>
  )
}

export default App
```
<br>
<h3>예제2</h3>

```jsx
# ProductCard.jsx
import styles from './Card.module.css'

const ProductCard = ({ 
  name, price, formatPrice /* string, number, function */
}) => {
  const displayedPrice
   = formatPrice(price)

  return (
    <div className={styles.card}>
      <h2>{name}</h2>
      <p>Price: {displayedPrice}</p>
    </div>
  );
}

export default ProductCard
```
```jsx
# App.jsx
import './App.css'

import ProductCard from './ProductCard'

const App = () => {
  const product = { 
    name: "Laptop", 
    price: 123.4567 
  };

  return (
    <ProductCard 
      name={product.name}
      price={product.price}
      formatPrice={(p) => `$ ${p.toFixed(2)}`}
    />
  );

  /* 이렇게 편하게 변환 */
  return (
    <ProductCard 
    {...product} 
    formatPrice={(p) => `$ ${p.toFixed(2)}`} 
    />
  );
}

export default App
```

<br>
<h3>예제2</h3>

```jsx
 # CardLayout.jsx
import styles from './Card.module.css'

const CardLayout = ({ 
  title, children 
}) => (
  <div className={styles.card}>
    <h2>{title}</h2>
    <div className="content">
      {children}
    </div>
  </div>
)

export default CardLayout

```
`App.jsx`
```jsx
import './App.css'
import CardLayout from './CardLayout';

const App = () => (
  <div>
    <CardLayout title="About">
      <p>Props of Components</p>
    </CardLayout>

    <CardLayout title="Details">
      <ul>
        <li>Feature A</li>
        <li>Feature B</li>
        <li>Feature C</li>
      </ul>
    </CardLayout>

    <CardLayout title="Contact">
      <p>Email: example@example.com</p>
      <p>Phone: 123-456-7890</p>
    </CardLayout>
  </div>
);

export default App
```
<br>
<h3>예제3 - 고차함수</h3>


`withConditionalCard.jsx`
```jsx
import styles from './Card.module.css'

function withConditionalCard(WrappedComp) {
  return function ConditionalCard({  /* 반환함수가 대문자의미 = 컴포넌트 */
    disabled, ...props 
  }) {
    const cardStyle = {
      opacity: disabled ? 0.5 : 1,
    }

    return (
      <div
        className={styles.card}
        style={cardStyle}
      >
        <WrappedComp {...props} />
      </div>
    )
  }
}

export default withConditionalCard
```

`SimpleCard.jsx`
```jsx
function SimpleCard({ title, content }) {
  return (
    <div>
      <h2>{title}</h2>
      <p>{content}</p>
    </div>
  )
}

export default SimpleCard
```
`App.jsx`

```jsx
import './App.css'

import withConditionalCard from './withConditionalCard'
import SimpleCard from './SimpleCard'

const ConditionalSimpleCard = withConditionalCard(SimpleCard)

const App = () => (
  <>
    <ConditionalSimpleCard 
      title="Active Card" 
      content="This card is active." 
      disabled={false} 
    />
    
    <ConditionalSimpleCard 
      title="Disabled Card" 
      content="This card is disabled." 
      disabled={true} 
    />
  </>
)

export default App
```
