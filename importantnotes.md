Q) <form><form/> why we use 'form' tag is it necessary to use form tag what happened if we didnt use form tag ?
**Ans** --> toh hum apne website me <form> use karte hai aur form toh use karenge hi kyuki hume apne users se information toh lenge hi aur information form ki help se hi lete hai toh us form ke data ko hum kisi backend me save karte hai toh jab hum form use karte iha toh hum apne pure form ke data ko submit kar dete hai backend me

फॉर्म डेटा को भेजना: अगर आप डेटा को बैकएंड पर भेजना चाहते हैं, तो सामान्यतः <form> का उपयोग करके आप onSubmit इवेंट का उपयोग कर सकते हैं। बिना <form> टैग के, आपको मैन्युअली fetch या axios का उपयोग करके डेटा को बैकएंड पर भेजना होगा।

<form> टैग के बिना फॉर्म सबमिशन कैसे करें
अगर आप <form> का उपयोग नहीं कर रहे हैं, तो आपको बटन पर एक onClick इवेंट हैंडलर जोड़ना होगा, जो मैन्युअली डेटा को बैकएंड पर भेजेगा:


<!--  Simple HTML me jab hum form submit karte hia  -->
**Simple Html me jab hum form submit karte hai**

lekin hum is tarike se **Reactjs** me form nahi submit karte kyuki jab hum is simple tarike se form submit karenge tab hamara page reload hoga , aur hum page reload na ho isisliye hum reactjs use karete hai
niche diye hue code ko run karke deheko reactjs aur jab aap submit karenge tab page reload hoga aur is tarike se ek aur dikkat hai ki isme form validation bhi nahi hota yani ki agar app ki inputs fields khali hai tab bhi apka form submit hojyega bhale ki apne data enter nahi kiya
import React from 'react'

const FormComponent = () => {
  return (
    <div style={{display:'flex',justifyContent:'center',alignItems:'center'}}>
    <div style={{backgroundColor:'lightpink',height:'500px',width:'500px',display:'flex' ,gap:'20px',flexDirection:'column',paddingInline:'50px',paddingTop:'50px'}}>
       <form action="">
<input style={{height:'50px'}} type="text" placeholder='Enter you email' />
<input style={{height:'50px'}} type="text" placeholder='Enter you password' />
   <button type='submit'>submit</button>
   </form>
    </div>
    </div>
  )
}

export default FormComponent

**Form Validation**
**1) Manually Form Validation**
 -> is me hum apne se hi form me validtion dete hai

**2)React Hook Form Validation** -> packages used for form validation


1) **Manually Form Validation**
isme hum khud se form me validtion karte hai har chiz khud hi karte hai 
niche diye code ko run karo aur dhekho

import React, { useState } from 'react';

const FormComponent = () => {
    const [email, setEmail] = useState('');
    const [password, setPassword] = useState('');
    const [errors, setErrors] = useState({});
    const [isSubmitting, setIsSubmitting] = useState(false);

    // वैलिडेशन फंक्शन
    const validate = () => {
        const newErrors = {};

        if (!email) {
            newErrors.email = 'ईमेल आवश्यक है';
        } else if (!/\S+@\S+\.\S+/.test(email)) {
            newErrors.email = 'अमान्य ईमेल';
        }

        if (!password) {
            newErrors.password = 'पासवर्ड आवश्यक है';
        } else if (password.length < 6) {
            newErrors.password = 'पासवर्ड कम से कम 6 अक्षर का होना चाहिए';
        }

        return newErrors;
    };

    // फॉर्म सबमिट करने पर
    const handleSubmit = (e) => {
        e.preventDefault();
        setIsSubmitting(true);

        const formErrors = validate();
        if (Object.keys(formErrors).length > 0) {
            setErrors(formErrors);
            setIsSubmitting(false);
            return;
        }

        console.log(email, password);

        setTimeout(() => {
            setIsSubmitting(false);
            alert('फॉर्म सफलतापूर्वक सबमिट हुआ!');
        }, 1000);
    };

    return (
        <div style={{ display: 'flex', justifyContent: 'center', alignItems: 'center', minHeight: '100vh', backgroundColor: '#f0f4f8' }}>
            <div style={{ backgroundColor: '#fff', padding: '40px', borderRadius: '8px', boxShadow: '0 4px 8px rgba(0, 0, 0, 0.1)', width: '400px' }}>
                <h2 style={{ marginBottom: '20px', color: '#333', textAlign: 'center' }}>लॉगिन फॉर्म</h2>
                <form onSubmit={handleSubmit}>
                    <div style={{ marginBottom: '20px' }}>
                        <input
                            value={email}
                            onChange={(e) => setEmail(e.target.value)}
                            type="text"
                            placeholder="ईमेल दर्ज करें"
                            style={{ width: '100%', padding: '10px', fontSize: '16px', borderRadius: '4px', border: '1px solid #ccc', boxSizing: 'border-box' }}
                        />
                        {errors.email && <p style={{ color: 'red', fontSize: '14px', marginTop: '5px' }}>{errors.email}</p>}
                    </div>

                    <div style={{ marginBottom: '20px' }}>
                        <input
                            value={password}
                            onChange={(e) => setPassword(e.target.value)}
                            type="password"
                            placeholder="पासवर्ड दर्ज करें"
                            style={{ width: '100%', padding: '10px', fontSize: '16px', borderRadius: '4px', border: '1px solid #ccc', boxSizing: 'border-box' }}
                        />
                        {errors.password && <p style={{ color: 'red', fontSize: '14px', marginTop: '5px' }}>{errors.password}</p>}
                    </div>

                    <button
                        type="submit"
                        disabled={isSubmitting}
                        style={{ width: '100%', padding: '10px', fontSize: '16px', color: '#fff', backgroundColor: '#007bff', border: 'none', borderRadius: '4px', cursor: 'pointer' }}
                    >
                        {isSubmitting ? 'प्रस्तुत हो रहा है...' : 'प्रस्तुत करें'}
                    </button>
                </form>
            </div>
        </div>
    );
};

export default FormComponent;





2) **React Hook Form Validation**


toh form validation ke liye hum bohot sare alag library ka use karte hai jaisa 'React Hook Form Validation' aur 'Formik' vagera in library use karne ke bohot sare fayade hai jaisa hume validation ka login nahi likhna padta hia hum form validation me jo error message dhikhana hia vo hum bohot aasani dhikhata sakte hia aur bohot aasani se apne form me valdiation laga sakte hai hume jisse hum bohot kam code likhna padta hia 

for example -> jab aap real world projects banate ho tab form bohot bade hote hia jaisa example jab aap exam form bharte ho toh usme bohot sare fields hoti hai tab apko usme manually states bananae padte hia jaisa

[name,userName]=useState()
[email,setEmail]=useState()
[password,setPassword]=useState().................etc
ho aap kab tak har ek input field ke liye alag alag usestate banaoge manlo agar 100 fields hui toh kya 100 usestate banaoge toh is chiz se bachne ke liye hum 







<!-- Form submit in Reactjs and right way of doing the form submit  -->
**Form submit in Reactjs**
**right way of doing the form submit using reactjs**
is tarike se jab hum form submit karte hai tab hamara page reload nahi hota 
 React.js में फॉर्म सबमिट करना (हर इनपुट के लिए अलग-अलग स्टेट के साथ):
React में हम प्रत्येक इनपुट फ़ील्ड के लिए अलग-अलग स्टेट का उपयोग कर सकते हैं और onChange इवेंट हैंडलर के माध्यम से इनपुट फ़ील्ड्स को अपडेट कर सकते हैं। उदाहरण के लिए
niche diye hue code ko run karo aur jab aap form submit karoge tab apka page reload nahi hoga , is code se page relaod nahi hoga 

import React, { useState } from 'react';

const FormComponent = () => {
    const [email, setEmail] = useState('');
    const [password, setPassword] = useState('');

    const handleSubmit = (e) => {
        // Page reload होने से रोकें
        e.preventDefault();
        // फॉर्म सबमिट होने पर ही दोनों वैल्यू कंसोल में आएंगी
        console.log(email, password);
    };

    return (
        <div style={{ display: 'flex', justifyContent: 'center', alignItems: 'center' }}>
            <div style={{ backgroundColor: 'lightpink', height: '500px', width: '500px', display: 'flex', gap: '20px', flexDirection: 'column', paddingInline: '50px', paddingTop: '50px' }}>
                <form onSubmit={handleSubmit}>
                    <input
                        value={email}
                        onChange={(e) => setEmail(e.target.value)}
                        type="text"
                        placeholder="Enter your email"
                    />
                    <input
                        value={password}
                        onChange={(e) => setPassword(e.target.value)}
                        type="text"
                        placeholder="Enter your password"
                    />
                    <button type="submit">Submit</button>
                </form>
            </div>
        </div>
    );
};

export default FormComponent;



----> kyu hume 2 wala tarika reactjs me hum jaisa form me state use karte hai vo takrika best kyu hia ?

आपका सवाल बहुत अच्छा है! चलिए समझते हैं कि React.js में फॉर्म हैंडलिंग के लिए स्टेट आधारित तरीका क्यों उपयोग किया जाता है, जबकि साधारण HTML फॉर्म (`<form>`, `<input>`, आदि) भी React.js में काम कर सकता है। 

### HTML फॉर्म (`<form>` टैग) का उपयोग React में:
1. **डिफ़ॉल्ट सबमिशन**: 
   - HTML फॉर्म को डायरेक्ट सबमिट करने पर, पेज रीलोड होता है और डेटा एक HTTP रिक्वेस्ट के माध्यम से बैकएंड पर भेजा जाता है।
   - यह तरीका सिंपल और छोटे अनुप्रयोगों के लिए ठीक है, लेकिन React में, यह तरीका बहुत सीमित है क्योंकि React स्पा (Single Page Application) है।

2. **पेज रीलोडिंग की समस्या**:
   - जब आप HTML फॉर्म को डायरेक्ट सबमिट करते हैं, तो पेज रीलोड होता है। इस रीलोडिंग के कारण आपकी मौजूदा एप्लिकेशन की स्टेट (जैसे कि यूज़र इंटरफ़ेस की स्थिति) खो जाती है।
   - React एक SPA है जो बिना पेज रीलोड किए यूज़र इंटरफेस को अपडेट करने के लिए जानी जाती है। इसलिए, पेज रीलोडिंग React एप्लिकेशन के लिए सही नहीं होती।

### निष्कर्ष:
- HTML में फॉर्म सबमिट करना तब उपयोगी होता है जब आप सिंपल और डायरेक्ट फॉर्म हैंडलिंग करना चाहते हैं, और आपको पेज रीलोडिंग से कोई समस्या नहीं होती।
- लेकिन React में स्टेट आधारित फॉर्म हैंडलिंग आपको फॉर्म के डेटा, वेलिडेशन, और सबमिशन प्रोसेस पर ज्यादा कंट्रोल देती है, जो एक अच्छा यूज़र अनुभव प्रदान करता है। यह आपके ऐप को एक सिंगल पेज एप्लिकेशन के रूप में बनाए रखने में मदद करता है, जो कि React का एक प्रमुख लाभ है।

### उदाहरण:
React में स्टेट आधारित फॉर्म हैंडलिंग करके आप यूज़र को रियल-टाइम वेलिडेशन मैसेज दिखा सकते हैं, बिना पेज को रीलोड किए। साथ ही, फॉर्म सबमिट होने के बाद आप डेटा प्रोसेसिंग और UI अपडेट आसानी से कर सकते हैं।

इसलिए, जब आप React में काम कर रहे होते हैं, तो स्टेट आधारित फॉर्म हैंडलिंग एक आदर्श तरीका है, जबकि सिंपल HTML फॉर्म का तरीका सीमित और कम लचीला है।


**React Form Validation**
Reack Form Hook package ye package hai form validation ke liye yani jaisa humne apna form bana liya completeley lekin hume form me validation bhi karna padta hia ki again input field khali hia toh ye error dhikhao aur agar hum toh agar hum ye packages use nahi karnge tab hume validation ka login calag alag se likhna padega toh us validation error ke code likhen se bachne ke liye hum ye third party packages use karte hia 

niche diye hue code ko run karo isme humne 'Reack Hook Form' use kiya hai

import React from 'react';
import { useForm } from 'react-hook-form'; // React Hook Form का इम्पोर्ट

const FormComponent = () => {
    const { register, handleSubmit, formState: { errors, isSubmitting }, reset } = useForm(); // React Hook Form से methods को extract किया

    // सबमिट फंक्शन
    const onSubmit = (data) => {
        console.log(data);
        
        // फॉर्म सबमिट के बाद रीसेट करें
        setTimeout(() => {
            reset();
            alert('फॉर्म सफलतापूर्वक सबमिट हुआ!');
        }, 1000);
    };

    return (
        <div style={{ display: 'flex', justifyContent: 'center', alignItems: 'center', minHeight: '100vh', backgroundColor: '#f0f4f8' }}>
            <div style={{ backgroundColor: '#fff', padding: '40px', borderRadius: '8px', boxShadow: '0 4px 8px rgba(0, 0, 0, 0.1)', width: '400px' }}>
                <h2 style={{ marginBottom: '20px', color: '#333', textAlign: 'center' }}>Login Form</h2>
                
                {/* handleSubmit से फॉर्म को सबमिट और वैलिडेट किया */}
                <form onSubmit={handleSubmit(onSubmit)}> 
                    <div style={{ marginBottom: '20px' }}>
                        {/* register method से इनपुट फील्ड को कनेक्ट किया */}
                        <input
                            {...register('email', { required: 'Email is required', pattern: { value: /\S+@\S+\.\S+/, message: 'Invalid email' } })}
                            type="text"
                            placeholder="Enter the email"
                            style={{ width: '100%', padding: '10px', fontSize: '16px', borderRadius: '4px', border: '1px solid #ccc', boxSizing: 'border-box' }}
                        />
                        {/* एरर मैसेज */}
                        {errors.email && <p style={{ color: 'red', fontSize: '14px', marginTop: '5px' }}>{errors.email.message}</p>}
                    </div>

                    <div style={{ marginBottom: '20px' }}>
                        {/* register method से पासवर्ड इनपुट कनेक्ट किया */}
                        <input
                            {...register('password', { required: 'Password is reruired', minLength: { value: 6, message: 'Password should at least 6 characters' } })}
                            type="password"
                            placeholder="Enter the Password"
                            style={{ width: '100%', padding: '10px', fontSize: '16px', borderRadius: '4px', border: '1px solid #ccc', boxSizing: 'border-box' }}
                        />
                        {/* एरर मैसेज */}
                        {errors.password && <p style={{ color: 'red', fontSize: '14px', marginTop: '5px' }}>{errors.password.message}</p>}
                    </div>

                    {/* सबमिट बटन */}
                    <button
                        type="submit"
                        disabled={isSubmitting}
                        style={{ width: '100%', padding: '10px', fontSize: '16px', color: '#fff', backgroundColor: '#007bff', border: 'none', borderRadius: '4px', cursor: 'pointer' }}
                    >
                        Submit
                    </button>
                </form>
            </div>
        </div>
    );
};

export default FormComponent;

1)React Hook Form का उपयोग: हमने useForm से register, handleSubmit, और formState को इम्पोर्ट किया।
2)register: इस method से इनपुट फील्ड्स को React Hook Form से कनेक्ट किया। इसमें वैलिडेशन के लिए रूल्स दिए गए हैं (जैसे ईमेल और पासवर्ड की वैलिडेशन)।
3)handleSubmit: यह method फॉर्म को सबमिट और वैलिडेट करने के लिए उपयोग होता है।
एरर हैंडलिंग: {errors.email && ...} का उपयोग करके एरर मैसेज दिखाए गए हैं।

**Important Question**
jaisa react form hook me register methiod hota hia vaisa kya login method bhi hota hai kya aur register agar nahi lhota toh login method kyu nahi hota kya hum keval resigter metod hi use karenge aur kya resitermehto dse keval register hi karte hia kya resgite mehtod se login nhai lkar sakte tel me in hindi?

नहीं, `react-hook-form` में कोई `login` नाम का method नहीं होता है। `react-hook-form` का मुख्य उद्देश्य फॉर्म की वैलिडेशन और डेटा मैनेजमेंट को आसान बनाना है। इसलिए इस लाइब्रेरी में एक ही method होता है जिसे `register` कहा जाता है। 

### `register` Method क्या करता है?

`register` method किसी भी इनपुट फील्ड (जैसे, ईमेल, पासवर्ड, आदि) को `react-hook-form` के साथ कनेक्ट करता है ताकि आप फॉर्म की वैल्यू और वैलिडेशन को ट्रैक कर सकें। इसका मतलब यह नहीं है कि यह सिर्फ "रजिस्टर" करने के लिए ही है। आप इसे किसी भी प्रकार के फॉर्म में उपयोग कर सकते हैं, चाहे वो रजिस्ट्रेशन फॉर्म हो, लॉगिन फॉर्म हो, कांटैक्ट फॉर्म हो, या कुछ और।

### तो `register` Method का नाम `login` क्यूं नहीं होता?

`register` method का नाम सिर्फ फॉर्म फील्ड्स को "रजिस्टर" करने के लिए है। इसका मतलब यह है कि हम उन फील्ड्स को ट्रैक और वैलिडेट कर रहे हैं। नाम का मतलब यहां लॉगिन या रजिस्ट्रेशन से नहीं है, बल्कि इनपुट फील्ड्स को फॉर्म के कंट्रोल में लाने से है। इसलिए, यह method किसी भी प्रकार के फॉर्म में इस्तेमाल किया जा सकता है।

### क्या `register` Method से लॉगिन कर सकते हैं?

हाँ, बिल्कुल! आप `register` method का उपयोग लॉगिन फॉर्म में भी कर सकते हैं। जैसे कि हमने पिछले उदाहरण में देखा था, हमने `register` method का उपयोग ईमेल और पासवर्ड फील्ड्स को कनेक्ट करने के लिए किया। इसका मतलब यह है कि आप `register` method से लॉगिन फॉर्म को भी ट्रैक और वैलिडेट कर सकते हैं।

इसलिए, जब भी आप `react-hook-form` का उपयोग करेंगे, आपको `register` method ही उपयोग करना पड़ेगा, चाहे वह लॉगिन फॉर्म हो या रजिस्ट्रेशन फॉर्म।

`errors.email` और `errors.password` वे ऑब्जेक्ट्स हैं जो `react-hook-form` की वैलिडेशन प्रोसेस के दौरान बनते हैं। जब आप इनपुट फील्ड्स को `register` method के साथ कनेक्ट करते हैं और कुछ वैलिडेशन रूल्स सेट करते हैं (जैसे कि ईमेल फील्ड में `required` और `pattern`), तो फॉर्म सबमिट करते समय अगर वैलिडेशन फेल होती है, तो ये `errors` ऑब्जेक्ट अपने-आप उन फील्ड्स के नाम से एरर स्टोर कर देता है।

### कैसे पता चलता है कि कोई एरर है?

- जब आप फॉर्म सबमिट करते हैं, `react-hook-form` पहले फील्ड्स की वैलिडेशन चेक करता है।
- अगर कोई वैलिडेशन फेल होती है, तो वह फील्ड का नाम (`email` या `password`) `errors` ऑब्जेक्ट में एरर मैसेज के साथ स्टोर हो जाता है।
- इसीलिए, जब आप `errors.email` लिखते हैं, तो यह चेक करता है कि `email` फील्ड में कोई एरर है या नहीं।
- अगर एरर है, तो वह मैसेज (`errors.email.message`) दिखाया जाता है।

इसलिए, `errors.email` और `errors.password` `react-hook-form` द्वारा बनाए गए ऑब्जेक्ट्स हैं जो हमें बताते हैं कि कोई एरर है या नहीं।