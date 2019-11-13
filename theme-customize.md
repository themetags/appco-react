# Template customization


## public
I hope you have seen this template `public` folder structure on [Folder structure](/folder-structure) menu.

In this `public` folder you can see `index.html` file. This file structure is like this-

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <!--meta, title, google fonts, all css linking here-->
</head>

<body>

  <div id="root"></div>
 
 <!--all js linking here-->
</body>

</html>
```

All HTML content will be load into this `div`:
```html
<div id="root"></div>
```




## entry points

##### index.js
Template `index.js` structure like this-
```js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

ReactDOM.render(<App />, document.getElementById('root'));

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.unregister();

```

##### app.js
Template `app.js` structure like this-
```js
import React from "react";
import { createStore } from "redux";
import { Provider } from "react-redux";
import AgencyCoApp from "./reducers";
import Routes from "./routers";

// create store
const store = createStore(
  AgencyCoApp
  // applyMiddleware(...middleware),
  // other store enhancers if any
);

function App() {
  return (
    <Provider store={store}>
      <Routes />
    </Provider>
  );
}

export default App;

```


## themes

`themes` folder included on `src` folder. You can check our folder structure on [Folder structure](/folder-structure) menu.
This is `theme` folder structure-
```text
|-- themes
    |-- theme1.js ( default theme)
    |-- theme2.js ( demo theme 2)
    .....
    |-- theme8.js ( demo theme eight )
    |-- about-us.js ( about us page )
    |-- services.js ( services page)
    |-- pricing.js ( pricing page )
    |-- contact.js ( contact page )
```

`theme` folder contain all of our 8 demos with other single page like `services`, `about-us`
etc.


## routes
In router section we used route js. where we linked all the route for our all theme. For routing we used react-router-dom.

```js
import React from "react";
import { BrowserRouter as Router, Route, Switch } from "react-router-dom";

// importing all the themes
import Theme1 from "../themes/theme1";
import Theme2 from "../themes/theme2";
import Theme3 from "../themes/theme3";
import Theme4 from "../themes/theme4";
import Theme5 from "../themes/theme5";
import Theme6 from "../themes/theme6";

export default class Routes extends React.PureComponent {
  render() {
    return (
      <React.Fragment>
        <Router>
          <Switch>
            <Route exact path="/" component={Theme1} />
            <Route exact path="/theme1" component={Theme1} />
            <Route exact path="/theme2" component={Theme2} />
            <Route exact path="/theme3" component={Theme3} />
            <Route exact path="/theme4" component={Theme4} />
            <Route exact path="/theme5" component={Theme5} />
            <Route exact path="/theme6" component={Theme6} />
          </Switch>
        </Router>
      </React.Fragment>
    );
  }
}

```


## components
Under components folder we wrote all of our components individually. 
We have written these components to make the developer’s life easy. 
By using these basic components, For example in our components directory there is `Header`, `HeroSection` , `footer` folder where we wrote our different styled component. For example `HeroSection` component-

### Component folder structure
```text
|-- components
    ....
    |-- HeroSection ( hero component folder )
        - index.js ( main demo hero section )
        - heroSection12.js ( demo two hero section )
        ...... ( and other )
        
    |-- Contact ( contact folder )
        - index.js 
        - ContactUs.js
    .
    ..
    ...    
```

### Contact Us component
`Contact/index.js`
```js
// improted modules
import React, { Component } from "react";
import { connect } from "react-redux";
import { submitContact } from "../../actions/index";
import _data from "../../data";

// Contact module
class Contact extends Component {
  constructor(props) {
    super(props);
    // state
    this.state = {
      name: "",
      email: "",
      phone: "",
      company: "",
      message: "",
      disableContactBtn: false,
      contactBtnText: "Send Message",
      contact: {}
    };

    this.handleSubmit = this.handleSubmit.bind(this);
  }

  /**
  * When we click on Send button, changeBtnText function will help to change text
  * @param contactBtnText
  */
  changeBtnText = contactBtnText => {
    this.setState({ contactBtnText });
  };

 /**
  * Get all form data and set to the state
  * @param contactBtnText
  */
  handleFormValueChange(inputName, event) {
    let stateValue = {};
    stateValue[inputName] =
      event.target.type === "checkbox"
        ? event.target.checked
        : event.target.value;
    this.setState(stateValue);
  }

 /**
  * Submit the form and dispatch to the store
  * @param contactBtnText
  */
  handleSubmit(event) {
    event.preventDefault();

    // disable the button
    this.setState({ disableContactBtn: true });

    // get action
    const contactAction = submitContact(this.state);

    // Dispatch the contact from data
    this.props.dispatch(contactAction);

    // added delay to change button text to previous
    setTimeout(
      function() {
        // enable the button
        this.setState({ disableContactBtn: false });

        // change to button name
        this.changeBtnText("Send Message");

        // get action again to update state
        const contactAction = submitContact(this.state);

        // Dispatch the contact from data
        this.props.dispatch(contactAction);

        // clear form data
        this.setState({
          name: "",
          email: "",
          phone: "",
          company: "",
          message: ""
        });
      }.bind(this),
      3000
    );
  }

  componentDidMount() {
    /**
     * Your ajax will goes here to get data then call setState
     */
    this.setState({
      contact: _data.contact
    });
  }

  render() {
    return (
      <React.Fragment>
        <section id="contact" className={"contact-us ptb-100 " + (this.props.bgColor && this.props.bgColor === 'white' ? '':  'gray-light-bg')}>
          <div className="container">
            <div className="row">
              <div className="col-md-5">
                <div className="section-heading">
                  <h3>{this.state.contact.title}</h3>
                  <p>{this.state.contact.description}</p>
                </div>
                <div className="footer-address">
                  <h6>
                    <strong>{this.state.contact.office}</strong>
                  </h6>
                  <p>{this.state.contact.address}</p>
                  <ul>
                    <li>
                      <span>Phone: {this.state.contact.phone}</span>
                    </li>
                    <li>
                      <span>
                        Email :{" "}
                        <a href="mailto:hello@yourdomain.com">
                          {this.state.contact.email}
                        </a>
                      </span>
                    </li>
                  </ul>
                </div>
              </div>
              <div className="col-md-7">
                <form
                  method="POST"
                  id="contactForm1"
                  className="contact-us-form"
                  noValidate="novalidate"
                  onSubmit={this.handleSubmit}
                >
                  <h5>Reach us quickly</h5>
                  <div className="row">
                    <div className="col-sm-6 col-12">
                      <div className="form-group">
                        <input
                          value={this.state.name}
                          onChange={e => this.handleFormValueChange("name", e)}
                          type="text"
                          className="form-control"
                          name="name"
                          placeholder="Enter name"
                          required="required"
                        />
                      </div>
                    </div>
                    <div className="col-sm-6 col-12">
                      <div className="form-group">
                        <input
                          value={this.state.email}
                          onChange={e => this.handleFormValueChange("email", e)}
                          type="email"
                          className="form-control"
                          name="email"
                          placeholder="Enter email"
                          required="required"
                        />
                      </div>
                    </div>
                  </div>
                  <div className="row">
                    <div className="col-sm-6 col-12">
                      <div className="form-group">
                        <input
                          value={this.state.phone}
                          onChange={e => this.handleFormValueChange("phone", e)}
                          type="text"
                          name="phone"
                          className="form-control"
                          id="phone"
                          placeholder="Your Phone"
                        />
                      </div>
                    </div>
                    <div className="col-sm-6 col-12">
                      <div className="form-group">
                        <input
                          value={this.state.company}
                          onChange={e =>
                            this.handleFormValueChange("company", e)
                          }
                          type="text"
                          name="company"
                          size="40"
                          className="form-control"
                          id="company"
                          placeholder="Your Company"
                        />
                      </div>
                    </div>
                  </div>
                  <div className="row">
                    <div className="col-12">
                      <div className="form-group">
                        <textarea
                          onChange={e =>
                            this.handleFormValueChange("message", e)
                          }
                          value={this.state.message}
                          name="message"
                          id="message"
                          className="form-control"
                          rows="7"
                          cols="25"
                          placeholder="Message"
                        ></textarea>
                      </div>
                    </div>
                  </div>
                  <div className="row">
                    <div className="col-sm-12 mt-3">
                      <button
                        type="submit"
                        className="btn primary-solid-btn"
                        id="btnContactUs"
                        disabled={this.state.disableContactBtn}
                        onClick={() => {
                          this.changeBtnText("Sending...");
                        }}
                      >
                        {this.state.contactBtnText}
                      </button>
                    </div>
                  </div>
                </form>
                <p className="form-message"></p>
              </div>
            </div>
          </div>
        </section>
      </React.Fragment>
    );
  }
}

/**
* connect() function connects a React component to a Redux store. 
* It provides its connected component with the pieces of the data it needs from the store, 
* and the functions it can use to dispatch actions to the store
*/
export default connect(state => ({
  state
}))(Contact);
```





## redux and reducers
Redux is a predictable state container for JavaScript apps.

It helps you write applications that behave consistently, run in different environments (client, server, and native), and are easy to test. On top of that, it provides a great developer experience, such as [live code editing combined with a time traveling debugger](https://github.com/reduxjs/redux-devtools).

You can use Redux together with React, or with any other view library. It is tiny (2kB, including dependencies), but has a large ecosystem of addons available.

### actions
Actions are payloads of information that send data from your application to your store. They are the only source of information for the store. You send them to the store using `store.dispatch()`.

Here is our defined actions:
```js
import { SUBSCRIBE, SUBMIT_CONTACT, POST_PROMO, GET_QUOTE } from '../constants/types.js';

export const subscribe = (email) => {
    return {
        type: SUBSCRIBE,
        email
    };
};

export const submitContact = (contactData) => {
    return {
        type: SUBMIT_CONTACT,
        contactData
    };
};

export const postPromo = (promoData) => {
    return {
        type: POST_PROMO,
        promoData
    };
};

export const getQuote = (quoteData) => {
    return {
        type: GET_QUOTE,
        quoteData
    };
};
```
### reducers
Reducers specify how the application's state changes in response to actions sent to the store. Remember that actions only describe what happened, but don't describe how the application's state changes.

Here is our reducer definition:
```js
import { SUBMIT_CONTACT, POST_PROMO } from '../constants/types.js';

const getContactData = (state, action) => {
    switch (action.type) {
        case SUBMIT_CONTACT:
            return {
                contactData: action.contactData
            };
        default:
            return state;
    }
}

const contact = (state = [], action) => {
    switch (action.type) {
        case POST_PROMO:
            return [...state, getContactData(undefined, action)];
        default:
            return state;
    }
};


export default contact;
```
quote

```js
import { GET_QUOTE } from '../constants/types.js';

const getQuoteData = (state, action) => {
    switch (action.type) {
        case GET_QUOTE:
            return {
                quoteData: action.quoteData
            };
        default:
            return state;
    }
}

const quote = (state = [], action) => {
    switch (action.type) {
        case GET_QUOTE:
            return [...state, getQuoteData(undefined, action)];
        default:
            return state;
    }
};


export default quote;
```

Subscribe 

```js
import { SUBSCRIBE } from '../constants/types.js';

const getEmail = (state, action) => {
    switch (action.type) {
        case SUBSCRIBE:
            return {
                email: action.email
            };
        default:
            return state;
    }
}

const subscribe = (state = [], action) => {
    switch (action.type) {
        case SUBSCRIBE:
            return [...state, getEmail(undefined, action)];
        default:
            return state;
    }
};


export default subscribe;
```

We have combined all reducers by following:
```js
import { combineReducers } from 'redux';
import contact from './contact';
import promo from './promo';
import quote from './quote';

import subscribe from './subscribe';

export default combineReducers({
    subscribe,
    contact,
    promo,
    quote
});


```

### data
Static content comes from this `data` folder like promo section content. If you want to get data from REST api call then you can use Saga, Thung or other side effects library.
Here is this structure-

```js
module.exports = {
  hero: {
      title: "Brainstorming for desired perfect Usability",
      description:
        "Our design projects are fresh and simple and will benefit your business greatly. Learn more about our work!",
      bgImage: "img/app-hero-bg.jpg"
    },
    promo: {
      title: "Why small business owners love AppCo?",
      description:
        "Following reasons show advantages of adding AgencyCo to your lead pages, demos and checkouts",
      items: [
        {
          title: "Clean Design",
          description:
            "Increase sales by showing true dynamics of your website",
          icon: "ti-vector text-white"
        },
        {
          title: "Secure Data",
          description:
            "Build your online store’s trust using Social Proof & Urgency",
          icon: "ti-lock text-white"
        },
        {
          title: "Retina Ready",
          description:
            "Realize importance of social proof in customer’s purchase decision",
          icon: "ti-eye text-white"
        }
      ]
    },
    aboutUs: {
      ...
    },
  ...
};
```




