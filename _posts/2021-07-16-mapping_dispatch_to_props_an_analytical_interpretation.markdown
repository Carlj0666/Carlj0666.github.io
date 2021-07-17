---
layout: post
title:      "Mapping Dispatch to Props: An analytical interpretation."
date:       2021-07-16 20:41:26 -0400
permalink:  mapping_dispatch_to_props_an_analytical_interpretation
---


![](https://upload.wikimedia.org/wikipedia/commons/7/70/Rorschach_blot_01.jpg)

Mapping dispatch to props allows us to make *action dispatching functions, as props* which can then be passed to and used inside our component. Let's examine this idea further:
```
1 const mapDispatchToProps = (dispatch) => {
2    return {
3         fetchInkblots: () => dispatch(fetchInkblots)
4     }
5 }
6
7 export default connect(mapStateToProps, mapDispatchToProps)(InkblotList)
```
*In line 7 dispatch is made available via connect, to mapDispatchToProps. Dispatch is then passed into mapDispatchToProps as an argument on line 1. We are returning an object, with a function for it's value, that function dispatches an action when called.*


![](https://i.imgur.com/PxAdLAm.png)

*You can see in the image above, that calling fetchInkblots in the console returns a function that itself contains a dispatch.*

```
1 export const fetchInkblots = 
2         (dispatch) => {
3         dispatch({type: 'LOADING'})
4         fetch(url)
5         .then(resp => resp.json())
6         .then(json => {
7             const inkblots = json.data
8             dispatch(setInkblots(inkblots))
9             })
10        }
```
*fetchInkblots can now dispatch actions as you see above in line 3*


By defining **fetchInkblots** inside of our mapDispatchToProps, like in the first code snippet, we can then execute it by referencing it as a **prop** since we have mapped this dispatch...to props : ):

```
 this.props.fetchInkblots()
```

I have a similar setup in my **<Form />** component, where a new inkblot is created:

```
1 const mapDispatchToProps = (dispatch) => {
2     return {
3         createInkblots: (inkblot) => dispatch(createInkblots(inkblot))
4     }
5 }

export default connect(null, mapDispatchToProps)(ImageForm)
```

In line 3 in the mapDispatchToProps, the **inkblot** is being passed in as a parameter to the createInkblots function. in this case, the parameter was submitted via the form in the handleSubmit below, **inkblot** represents the **state** of the form, passed in as **this.state** in line 4 of the handleSubmit.. 

In my handleSubmit in the <Form />, you can see **createInkblots** being referenced as a prop. From here createInkblots is fired off...

```
1 handleSubmit = (event) => {
2         event.preventDefault()
3 
4         this.props.createInkblots(this.state)
```

**Back in the actions folder**

```
1 export const createInkblots = (inkblot) => {
2     return (dispatch) => {
3         const configObj = {
4             method: 'POST',
5             headers: {
6                 "Content-Type": "application/json",
7                 "Accepts": "application/json"
8             },
9             body: JSON.stringify(inkblot)
10         }
11         
12        fetch(url, configObj)
13         .then(resp => resp.json())
14         .then(json => {
15             const newinkblot = json.data
16             dispatch(addInkblot(newinkblot))
17         })
18     }
```

From line 18 we dispatch the **addInkblot** action, which itself takes in the newly returned json, which then hits the reducer, state is updated and the re-render occurs, thus displaying the new inkblot.

## Go forth and mapDispatchToProps!

*[For more in depth analysis](https://stackoverflow.com/questions/34458261/how-to-get-simple-dispatch-from-this-props-using-connect-w-redux)*
		

