# 3. code refactoring

- script.js

```js
//code refactoring

//get element
const form = document.getElementById('form');
const username = document.getElementById('username');
const email = document.getElementById('email');
const password = document.getElementById('password');
const passwrod2 = document.getElementById('password2');

//show input error input
const showError = (input, message) => {
    const formControl = input.parentElement;
    formControl.className = 'form-control error';
    const small = formControl.querySelector('small');
    small.innerText = message;
}

//show success
const showSuccess = (input) => {
    const formControl = input.parentElement;
    formControl.className = 'form-control success';
}

//check email if it is valid
const isValidEmail = (email) => {
    const result = /^([A-Za-z0-9_\-\.])+\@([A-Za-z0-9_\-\.])+\.([A-Za-z]{2,4})$/;
    //这是一个邮箱的regular expression
    return result.test(String(email));
}

//check Required input
const checkRequired = (inputArrary) => {
    inputArrary.forEach((input) => {
        // console.log(input.value);
        (input.value.trim() === '') ? showError(input, `${getKeyWords(input)} must be filled`) : showSuccess(input);
    });
}

//get keyWords
const getKeyWords = (input) => {
    return input.placeholder.slice(6); //skip first 6 chars 
}

//event listening
form.addEventListener('submit', (e) => {
    e.preventDefault(); //注册表单，会默认表单事件，console.log 转瞬即逝，所以调用此函数
    // console.log(username.value);
    checkRequired([username, email, password, passwrod2]);
});
```

![](img/2020-04-05-04-08-40.png)