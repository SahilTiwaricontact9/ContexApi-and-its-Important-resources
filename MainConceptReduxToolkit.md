**Context Api ke liye Pyush garg ki video dhek log phale puri video dheklo bina sath me code likhe fir khud se code karo 100 ki sidhi bat**

pyush garg value ko phale apply karo fir vahi same chiz me useReducer ka use karo apne se pyush garp vale me humne direct login likh diya that button ke click pe but ab hum Reducer use karenge aur logic banayange 

toh pyush garg vala apply karke fir niche valal karo 
matlab same chiz ab hum reducer ka use karke karenge

Q) Diffrence between usestate and useReducer both are used to making the state and updating the state
What is useReducer used for?
The useReducer Hook is used to store and update states, just like the useState Hook. It accepts a reducer function as its first parameter and the initial state as the second. useReducer returns an array that holds the current state value and a dispatch function to which you can pass an action and later invoke it.

useReducer is very similar to useState, but it lets you move the state update logic from event handlers into a single function outside of your component. matlab
 ye hai second tarika jisme hum reducer use kar rahe hia 

Files ->
1) App.js
import React, { useContext } from 'react'
import CounterButtons from './components/CounterButtons'
import { mycounterContext } from './contexts/counterContext'

const App = () => {
  const a = useContext(mycounterContext)
  console.log(a.count)

  
  return (
    <div style={{display:'grid',justifyContent:'center',alignItems:'center'}}>
      <h1>Count is {a.count}</h1>
      <CounterButtons />
      <CounterButtons/>
      <CounterButtons/>
      <CounterButtons/>
    </div>
  )
}

export default App


2)CounterContext file
import { createContext, useReducer, useState } from "react";

export const mycounterContext=createContext(null)

// reducer function to handle diffrent actions
// this contextReducer will take two thing 'current state or initial state' and 'action or the logic to update the state'
export const contextReducer=(state,action)=>{
    switch(action.type){
        case "Increment":
            return state+1
        case "Decrement":
            return state-1
        default:// agar koi bhi action na ho toh kuch mat karo job hia vaisa hi rahena do
        return state;
    }
}



// provider ka name Capital letter se shuru hoga agar small se karoge toh error ayega
export const  MycontextProvider=(props)=>{
    // global state of counter
    const initialState=0;
    const [state, dispatch] = useReducer(contextReducer, initialState);
return (
    <mycounterContext.Provider value={{count:state,dispatch}}>
        {props.children}
    </mycounterContext.Provider>
)
}

3)Counterbuttons 
import React, { useContext } from 'react'
import { mycounterContext } from '../contexts/counterContext'

const CounterButtons = () => {
    const b = useContext(mycounterContext)

  return (
    <div>
        <button onClick={()=>b.dispatch({type:"Increment"})}>Increment</button>
        <button onClick={()=>b.dispatch({type:"Decrement"})}>Decrement</button>
    </div>
  )
}

export default CounterButtons

4)Index.js
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';
import { MycontextProvider } from './contexts/counterContext';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <MycontextProvider>
    <App />
    </MycontextProvider>
  </React.StrictMode>
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();




**`useState` aur `useReducer`` ek jaise nahi hain, lekin dono ka use state management ke liye hota hai.** Dono mein kuch differences hain, aur unka use case bhi alag hai. Chaliye, pehle un dono ke bare mein samajhte hain aur phir aapke prashna ka jawab dete hain.

### 1. **`useState`**:
- `useState` ek simple React hook hai jisse hum functional components ke andar state manage kar sakte hain.
- Yeh ek initial state leta hai aur ek array return karta hai jisme do values hoti hain: current state aur state update karne ka function (setter function).
- `useState` kaafi straightforward hai, lekin jab state management complex ho jati hai ya aapko ek se jyada states ko manage karna ho, toh isse thoda mushkil ho sakta hai.
- **Use case**: Choti aur simple states manage karne ke liye, jaisa ki form input, toggle state, counter, etc.

**Example:**
```jsx
const [count, setCount] = useState(0);

// State update
setCount(count + 1);
```

### 2. **`useReducer`**:
- `useReducer` thoda complex aur powerful hook hai. Yeh reducer pattern follow karta hai, jisme ek `reducer` function state aur action ko use karke new state return karta hai.
- `useReducer` ek initial state aur ek reducer function leta hai. Yeh state aur `dispatch` function return karta hai.
- **Use case**: Jab aapke paas complex state logic ho ya aapko ek hi jagah se multiple types ki state transitions handle karni ho. Yeh Redux jaisa lagta hai, lekin component level par use hota hai.

**Example:**
```jsx
const [state, dispatch] = useReducer(reducer, initialState);

// State update
dispatch({ type: 'INCREMENT' });
```

### **Difference aur Answer:**
1. **Kya `useState` aur `useReducer` same hai?** 
   - **Nahi**, yeh same nahi hain. `useState` simple aur choti states ke liye hota hai, jabki `useReducer` complex state logic handle karne ke liye hota hai. `useReducer` aapko ek reducer function define karne deta hai jisse aap different actions ke through state update kar sakte hain.

2. **Kya `useState` ko keval ek component me use kar sakte hain?** 
   - Ji haan, `useState` sirf wahi component me use hota hai jisme aapne usko define kiya hai. Agar aapko kisi aur component me usi state ki jarurat hai, toh aapko `props` pass karne padenge ya context (`useContext`) use karna padega.

3. **Kya `useReducer` se hum state update kar sakte hain bina us jagah se?** 
   - Ji haan, `useReducer` ko aap context ke sath use kar sakte hain jaisa ki aapne code me kiya hai. Isme aapne `mycounterContext` banaya hai jisse aap state aur `dispatch` function ko kisi bhi component me use kar sakte hain.
   - `useReducer` ko context ke sath wrap karke aap state ko multiple components me use kar sakte hain bina unko directly update kiye. Bas aapko context se state aur `dispatch` function lena hota hai aur actions (`dispatch({ type: 'INCREMENT' })`) bhejna hota hai.

**Samjhen:**
- **`useState`** sirf usi component me use hota hai jaha define kiya hai.
- **`useReducer`** context ke sath use karke aap us state ko dusre components me bhi access aur update kar sakte hain, bina directly us jagah useState define kiye. 

### **Jab aapke case me `useReducer` useful ho sakta hai:**
- Agar aapke pass multiple buttons ya components hain jo ek hi state ko update karte hain, jaise ki increment, decrement, reset, etc., toh `useReducer` in sab state updates ko handle karne ke liye ek centralized jagah provide karta hai.

Toh, `useState` aur `useReducer` dono useful hain, lekin unke use cases alag-alag hain. Simple states ke liye `useState` sahi hai, aur complex ya multiple states ko manage karne ke liye `useReducer` ko context ke sath use karna better hota hai.


**Why should we use Redux Toolkit**.
<!-- Important topics to understand redux toolkit -->
***Important Phases to understand Redux Toolkit***

**Examples :Add to Cart Functionallity **

**1)** -> ***Implement 'Add to cart' functionality without using any library even dont use 'Context Api'***

Methods to implement 1) question 
we have two methods 

**method** **1** We will create the state in Parent Component and then we will pass that that state as a Prop and when anybody clik on the button we will just update that state

<!-- Implementation -->
Files -> 1) App.jsx
         2) Home.jsx
         3) Header.jsx

**1) App.jsx**
 import React, { useState } from 'react'
import Header from './Components/Header'
import Home from './Components/Home'

const App = () => {
  const [count, setCount] = useState(0)
  return (
    <div>
      <Header count={count} />
      <Home count={count} setCount={setCount} />
    </div>
  )
}

export default App

**2) Home.jsx**
import React from 'react'

const Home = ({count,setCount}) => {

  const onClickButton=()=>{
    setCount(count+1)
  }
  return (
    <div>

<div style={{ padding: '20px' }}>
      <div style={{ display: 'grid', gridTemplateColumns: 'repeat(3, 1fr)', gap: '20px' }}>
        {/* 1 card */}
        <div style={{
          border: '1px solid #ddd',
          padding: '10px',
          borderRadius: '8px',
          textAlign: 'center',
        }}>
          <img
            src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcStPb9AO5Asho7-twtDhUTFugN5RGM5X3OWxg&s"
            alt="Product"
            style={{ width: '100%', height: 'auto', marginBottom: '10px' }}
          />
          <h3 style={{ marginBottom: '10px' }}>Product Name</h3>
          <button onClick={onClickButton} style={{
            backgroundColor: '#28a745',
            color: 'white',
            border: 'none',
            padding: '10px 15px',
            cursor: 'pointer',
            borderRadius: '4px',
          }}>
            IPhone
          </button>
        </div>
        {/* 2 card */}
        <div style={{
          border: '1px solid #ddd',
          padding: '10px',
          borderRadius: '8px',
          textAlign: 'center',
        }}>
          <img
            src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcStPb9AO5Asho7-twtDhUTFugN5RGM5X3OWxg&s"
            alt="Product"
            style={{ width: '100%', height: 'auto', marginBottom: '10px' }}
          />
          <h3 style={{ marginBottom: '10px' }}>Product Name</h3>
          <button onClick={onClickButton} style={{
            backgroundColor: '#28a745',
            color: 'white',
            border: 'none',
            padding: '10px 15px',
            cursor: 'pointer',
            borderRadius: '4px',
          }}>
            IPhone
          </button>
        </div>

        {/* Duplicate this card structure for other products as needed */}
        {/* Add more cards here */}
      </div>
    </div>
    </div>
  )
}

export default Home


**3) Header.jsx**

import React from 'react'

const Header = ({count}) => {
  return (
    <div>
        
        <header style={{ display: 'flex', justifyContent: 'space-between', alignItems: 'center', padding: '10px', backgroundColor: '#f8f9fa' }}>
      <div style={{ fontSize: '24px', fontWeight: 'bold' }}>ShopName</div>
      <div style={{ position: 'relative' }}>
        <i className="fas fa-shopping-cart" style={{ fontSize: '24px', cursor: 'pointer' }}></i>
        <span style={{
          position: 'absolute',
          top: '-8px',
          right: '-8px',
          backgroundColor: 'red',
          color: 'white',
          borderRadius: '50%',
          padding: '4px 8px',
          fontSize: '12px',
          fontWeight: 'bold',
        }}>
          {count} {/* This is where the total cart item count will be displayed */}
        </span>
      </div>
    </header>
    </div>
  )
}

export default Header




**method 2** **2** -> In This we didn't create any global state and i had maked the state in home page or in cards container page and then click on ***add to cart*** button and then the value of cart increases and we had two componetn only 'Home' page in which we had all teh cards and other is 'Header' Component in which the cart icon is there

**Ans** No, we  don't do this using states
 
 aur yani par hume 'Context Api' use karna padta hai 






**Context Api** -> toh uper jo problem aa rai thi bo problem solve karne ke liye hi hum 'Context Api' ya fir koi extenral State management library use karte hai Let's understand the context api 

toh agar hume koi aisa state banane ho jisse hum multiple component me use karna hai toh hum us ke liye global state banate hai context api ka use karke
toh context api se hum global state banate hai aur fir usse apne kisi bhi component me us karte hai

Basics terms

1) createContext -> createContext se hum apne context ko banate hai,ye bhi hume react hi provide karta hai


2) useContext-> useContext() hook se hum apne banaye hue context ko use kar sakte hai kisi bhi component me , bina useContext ke hum apne banaye hue contenxt ko use nahi kar sakte hai ,useContext function bhi hume react hi deta hai 

3) useProvider = useProvider hamare context ko globaly banata hai jab hum apne useReducer function se kisi bhi state ko update karte hai toh vo updated state show karegi with the help of useProvider agar hume Provider ko use nahi kiya tab kuch bhi update hoga state me fir bhi hum nahi dhek payenge

4) useReducer = useReducter login controller hai hai iske ander hamara logic hota hai ye humara function hota hai jise hum 'reducer functon bolte hai'
useReducer का उपयोग करें ताकि आप context की value को dynamically change कर सकें।
5) Dispatch=dispatch: Yeh ek function hai jiska use hum reducer ko actions bhejne ke liye karte hain. Jab bhi aapko state update karni ho, aap dispatch ko call karte hain aur action pass karte hain. Phir yeh dispatch action ko reducer tak pahunchata hai, jisse state update hoti hai.
6) action =Action aur Dispatch me Antar:
Action (क्रिया): Yeh ek object hai jisme hum action ki type aur data define karte hain. Yeh batata hai ki state ko kaise update karna hai.
Example: { type: 'INCREMENT' } ek action hai jisse hum state me count ko increment karne ko keh rahe hain.
Dispatch (प्रेषण): Yeh ek function hai jiska kaam action ko reducer tak pahunchana hai. Jab hum dispatch call karte hain, tab reducer function execute hota hai aur us action ke basis par state update karta hai.

What is useReducer used for?
The useReducer Hook is used to store and update states, just like the useState Hook. It accepts a reducer function as its first parameter and the initial state as the second. useReducer returns an array that holds the current state value and a dispatch function to which you can pass an action and later invoke it.



### Provider और Reducer का काम शॉपिंग कार्ट के उदाहरण से समझें

#### 1. **Provider का काम:**
`Provider` एक React कॉम्पोनेन्ट है जो कि पूरे ऐप को ग्लोबल स्टेट प्रदान करता है। इसे आमतौर पर `Context API` या `Redux` के साथ उपयोग किया जाता है। Provider का मुख्य काम है कि वह सारे कॉम्पोनेन्ट्स (चाहे वो कितने भी nested हों) को एक स्टेट या डेटा प्रोवाइड कर सके।

**शॉपिंग कार्ट उदाहरण:**

मान लीजिए कि आपके पास एक शॉपिंग कार्ट है, जिसमें आपको यह जानना है कि कितने आइटम्स कार्ट में हैं, उनके नाम, कीमतें, और कुल राशि। 

अब, यह सारी जानकारी अलग-अलग कॉम्पोनेन्ट्स में चाहिए होगी:
- `Header` में कुल आइटम्स की संख्या दिखानी है।
- `Cart` पेज पर आइटम्स की लिस्ट और कुल राशि दिखानी है।
- `Product` पेज पर "Add to Cart" बटन से आइटम जोड़ने की सुविधा चाहिए।

हर जगह इस जानकारी को इस्तेमाल करने के लिए हमें एक ग्लोबल स्टेट चाहिए। इसी काम के लिए हम `Provider` का इस्तेमाल करते हैं। 

जब आप `Provider` का उपयोग करते हैं, तो आप अपने सारे कॉम्पोनेन्ट्स को एक ही जगह से स्टेट और डेटा पहुंचा सकते हैं। इस तरह, किसी भी कॉम्पोनेन्ट को अलग-अलग स्टेट रखने की जरूरत नहीं होती। 

#### 2. **Reducer का काम:**
`Reducer` एक फंक्शन है जो स्टेट को मैनेज करने में मदद करता है। यह एक प्रकार का लॉजिक कंट्रोलर है जो यह तय करता है कि स्टेट में क्या बदलाव होने चाहिए, और किस प्रकार होने चाहिए। इसमें दो मुख्य चीज़ें होती हैं: 
- **Current State:** जो अभी की स्थिति है।
- **Action:** जो बदलाव करना है।

`Reducer` एक नया स्टेट रिटर्न करता है, जिसे बाद में `Provider` के माध्यम से सभी कॉम्पोनेन्ट्स को उपलब्ध कराया जाता है।

**शॉपिंग कार्ट उदाहरण:**

शॉपिंग कार्ट में हम कुछ प्रमुख एक्शन्स करते हैं:
- आइटम्स को कार्ट में जोड़ना (`ADD_TO_CART`)
- आइटम्स को कार्ट से हटाना (`REMOVE_FROM_CART`)
- कुल राशि का अपडेट करना (`UPDATE_TOTAL`)

Reducer इन्हीं एक्शन्स को हैंडल करता है और तय करता है कि स्टेट में क्या बदलाव होना चाहिए।



यह `Reducer` एक फंक्शन है जो हर बार एक्शन मिलने पर नये स्टेट की गणना करता है। यहाँ `state` में दो चीज़ें हैं: `items` और `total`। जब हम `ADD_TO_CART` एक्शन भेजते हैं, तो यह फंक्शन स्टेट को अपडेट कर देता है।

#### **संक्षेप में:**

- **`Provider`:** यह एक wrapper है जो सारे कॉम्पोनेन्ट्स को एक ही स्टेट से जोड़ता है। यह उस स्टेट को सभी कॉम्पोनेन्ट्स में उपलब्ध कराता है ताकि वह हर जगह इस्तेमाल हो सके।
  
- **`Reducer`:** यह स्टेट को मैनेज करने वाला फंक्शन है। यह एक्शन के आधार पर स्टेट में बदलाव करता है, जैसे आइटम्स को कार्ट में जोड़ना या हटाना।

इन दोनों का उपयोग करने से हमारा शॉपिंग कार्ट ऐप सिंपल और मैनेज करने में आसान हो जाता है।


