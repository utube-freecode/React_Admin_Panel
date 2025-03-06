# React_Admin_Panel

## Console Logs Empty in Production
### index.js file React Project


import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import { Provider } from "react-redux";
import store from "./store/index";
import { persistedStore } from "./store/index";
import { PersistGate } from "redux-persist/integration/react";
import { BrowserRouter } from "react-router-dom";
import $ from "jquery";
import SocketContext, {
  _socket,
  scoresocket,
  DashboardSocket,
  MatchOddsSocket,
  FancySocket,
  BookMakerSocket,
  prefix,
} from "./contexts/socket";
import { AppProvider } from "./contexts/socketContext";
const root = ReactDOM.createRoot(document.getElementById("root"));

if (process.env.NODE_ENV === "production") {
  $("html").on("contextmenu", function (e) {
    return false;
  });
  console.log = () => {};
  console.error = () => {};
  console.debug = () => {};
  console.warn = () => {};

  if (typeof window.__REACT_DEVTOOLS_GLOBAL_HOOK__ === "object") {
    for (let prop in window.__REACT_DEVTOOLS_GLOBAL_HOOK__) {
      window.__REACT_DEVTOOLS_GLOBAL_HOOK__[prop] =
        typeof window.__REACT_DEVTOOLS_GLOBAL_HOOK__[prop] === "function"
          ? () => {}
          : null;
    }
  }
}

root.render(
  <Provider store={store}>
    <PersistGate loading={null} persistor={persistedStore}>
      <SocketContext.Provider
        value={{
          _socket: _socket,
          scoresocket: scoresocket,
          DashboardSocket: DashboardSocket,
          MatchOddsSocket: MatchOddsSocket,
          FancySocket: FancySocket,
          BookMakerSocket: BookMakerSocket,
          prefix: prefix,
        }}
      >
        <AppProvider>
          <BrowserRouter>
            <App />
          </BrowserRouter>
        </AppProvider>
      </SocketContext.Provider>
    </PersistGate>
  </Provider>
);




## Set Error when empty text field in React
### handleOnChangeTextField

const handlePasswordChange = (event) => {
    setTransactionPassword(event.target.value);
    seterrors({
      password: event.target.value === "" ? "Password is required" : "",
    });
  };

  const isValidForm = () => {
    if (!transactionPassword && transactionPassword === "") {
      seterrors((prev) => ({
        ...prev,
        password:
          !transactionPassword && transactionPassword === ""
            ? "Password is required"
            : "",
      }));
      return false;
    }
    return true;
  };

const handleSubmit = async (event) => {
    event.preventDefault();
    if (isValidForm()) {
      //API Call
  };


## Checkbox checked when includes
### input type checkbox in map

{sideLockData.map((sport, index) => (
                  <li key={sport._id} className="add_mche_card">
                    <input
                      id={`check_${sport._id}`}
                      type="checkbox"
                      checked={lockData
                        .map((lc) => lc.eventId)
                        .includes(sport._id)}
                      onChange={() => addDelSplortLock(sport._id, sport.name)}
                      value={sport._id}
                      className="form-check-input"
                    />
