Login Failed: bundle.js:381 [webpack-dev-server] Server started: Hot Module Replacement enabled, Live Reloading enabled, Progress disabled, Overlay enabled.
bundle.js:456 [HMR] Waiting for update signal from WDS...
index.js:112 Uncaught TypeError: Cannot read properties of null (reading 'addEventListener')
    at HTMLDocument.eval (index.js:112:16)
eval @ index.js:112
xhr.js:195 
            
            
           POST https://cors-anywhere.herokuapp.com/https://abhirebackend.onrender.com/auth/login 404 (Not Found)
(anonymous) @ xhr.js:195
xhr @ xhr.js:15
Nt @ dispatchRequest.js:51
value @ Axios.js:187
(anonymous) @ Axios.js:40
p @ axios.min.js:2
(anonymous) @ axios.min.js:2
(anonymous) @ axios.min.js:2
p @ axios.min.js:2
a @ axios.min.js:2
(anonymous) @ axios.min.js:2
r @ axios.min.js:2
(anonymous) @ Axios.js:63
(anonymous) @ Axios.js:226
e.<computed> @ bind.js:5
(anonymous) @ signin.html:357
signin.html:368  Login Failed: ye {message: 'Request failed with status code 404', name: 'AxiosError', code: 'ERR_BAD_REQUEST', config: {…}, request: XMLHttpRequest, …}code: "ERR_BAD_REQUEST"config: {transitional: {…}, adapter: Array(3), transformRequest: Array(1), transformResponse: Array(1), timeout: 0, …}message: "Request failed with status code 404"name: "AxiosError"request: XMLHttpRequest {onreadystatechange: null, readyState: 4, timeout: 0, withCredentials: false, upload: XMLHttpRequestUpload, …}response: {data: {…}, status: 404, statusText: 'Not Found', headers: r, config: {…}, …}status: 404stack: "AxiosError: Request failed with status code 404\n    at Ye (https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js:2:31710)\n    at XMLHttpRequest.y (https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js:2:36585)\n    at e.<anonymous> (https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js:2:48581)\n    at p (https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js:2:3448)\n    at Generator.<anonymous> (https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js:2:4779)\n    at Generator.throw (https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js:2:3858)\n    at p (https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js:2:9996)\n    at s (https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js:2:10235)"[[Prototype]]: Error
(anonymous) @ signin.html:368
signin.html:370 Uncaught (in promise) ReferenceError: response is not defined
    at HTMLButtonElement.<anonymous> (signin.html:370:23)
(anonymous) @ signin.html:370
