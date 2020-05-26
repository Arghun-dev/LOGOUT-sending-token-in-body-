# LOGOUT-sending-token-in-body-

### How to send just token in body in POST request in logout method:

```
// LOGOUT USER
export const logout = (token) => (dispatch, getState) => {

  const body = JSON.stringify({ token })

  axios
    .post("ws/api/Users/UserLogOut", body, tokenConfig(getState))
    .then((res) => {
      dispatch({
        type: LOGOUT_SUCCESS,
      });
    })
    .catch((err) => {
      console.log(err);
    });
};

// Setup config with token - helpr function
export const tokenConfig = (getState) => {
  // Get token from state
  const token = getState().auth.token;

  // Headers
  const config = {
    headers: {
      "Content-Type": "application/json",
    },
  };

  // If token, add to headers config
  if (token) {
    config.headers["Authorization"] = `Token ${token}`;
  }

  return config;
};
```
