Create a bar chart using html css
Create counting 
Settimeout  startcounting is this correct or incorrect (output useEffect wise)
```jsx
import React, { useState, useEffect } from 'react';

  

export default function App() {

  // [40, 400, 600, 60, 40, 700]

  

  return <ChartComponent chartData={[40, 400, 600, 60, 40, 700]} />;

}

  

function ChartComponent({ chartData }) {

  return (

    <div

      style={{

        // maxHeight: '500px',

        // width: '500px',

        borderBottom: '1px solid black',

        display: 'flex',

        flexDirection: 'row',

        gap: '10px',

      }}

    >

      {chartData?.map((item) => (

        <div

          style={{

            height: `${(10 * item )/ 10}px`,

            width: '50px',

            backgroundColor: 'blue',

            marginTop: 'auto',

          }}

        ></div>

      ))}

    </div>

  );

}

  

// export default function App() {

//   const [name, setName] = useState('India');

  

//   const handleEvent = () => {

//     setName('Bharat');

//   };

  

//   return (

//     <>

//       <button onClick={handleEvent}>

//         Click here

//       </button>

//       <h1>I am Parent</h1>

//       <span>{name}</span>

//       <Child name={name} />

//     </>

//   );

// }

  

// function Child({ name }) {

//   const [childName, setChildName] = useState(name);

//   useEffect(() => {

//     setChildName(name);

//   }, [name])

//   return (

//     <>

//       <h4>I am Child</h4>

//       <div>{childName}</div>

//     </>

//   );

// }

  

// function DelayedCounter() {

//   const [count, setCount] = useState(0);

//   const [btn, setBtn] = useState(false);

//   const startCounting = () => {

//     for (let i = 1; i <= 5; i++) {

//       setTimeout(() => {

//         setCount(count + i);

//       }, i * 1000);

//     }

//   };

//   const startCounting1 = () => {};

//   useEffect(() => {

//     if(!btn) return;

//     if(count === 5) return;

//     const id = setTimeout(() => {

//       setCount((prev) => prev + 1);

//     }, 1000);

//     return () => clearTimeout(id);

//   }, [btn, count]);

  

//   return (

//     <div>

//       <p>Count: {count}</p>

//       <button onClick={() => setBtn((prev) => !prev)}>Start Counting</button>

//     </div>

//   );

// }
```