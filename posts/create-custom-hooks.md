---
title: 'How to create custom react hooks'
date: '2022-09-13'
---

If you're anything like me, creating your own react hook sounds a bit intimidating, but to my surprise you don't need to be the next Dan Abramov to create your own hooks. In this article we'll discuss why creating your own hooks could be useful, and walk through a couple practical examples.

## Why create custom hooks in react? ##

As programmers we always hear to keep code DRY. Being able to reuse logic throughout our application **saves time** and **removes unnecessary clutter**. 

Let's look at an example. 

    const handleInputChange = (e) => {
        setFormData({ ...form, [e.target.name]: e.target.value });
    };

There is a good chance you have seen or written a function like this in order to update state when using a form. If our application only has one form, then this is no big deal, but in many cases our applications can have **many** forms. It's not very DRY of us to write this same function in every component that uses a form write?

## Implementing a custom hook ##

Let's create a custom reusable hook for managing state when dealing with form input. 

```
import React, {useState} from 'react'
const useForm = (initialState = {}) => {
    const [formData, setFormData] = useState(initialState);

    const handleInputChange = (e) => {
        setFormData({ ...formData, [e.target.name]: e.target.value })
    }

    return { formData, handleInputChange };
}

```
**Our new custom hook used in a form component**
```c
const LoginForm = () => {
    const { formData, handleInputChange } = useForm(
        {
            username: "",
            password: "",
        },
        (formData) => console.dir(formData)
    );

    const { username, password } = formData;

    return (
        <form onSubmit={handleSubmit}>
            <input
                type="text"
                name="username"
                value={username}
                onChange={handleInputChange}
            />
            <input
                type="password"
                name="password"
                value={password}
                onChange={handleInputChange}
            />
            <button type="submit">Submit</button>
        </form>
    );
}
```
**Note** we could also add a handleInput function in our useForm hook

