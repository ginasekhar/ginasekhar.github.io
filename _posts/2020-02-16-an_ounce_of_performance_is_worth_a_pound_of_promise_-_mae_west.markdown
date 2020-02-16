---
layout: post
title:      "An ounce of performance is worth a pound of promises - Mae West"
date:       2020-02-16 10:27:18 -0500
permalink:  an_ounce_of_performance_is_worth_a_pound_of_promise_-_mae_west
---


For my Javascript/Rails API project, I created a Single Page Application that allows a user to create a list of destinations they would like to visit and the attractions corresponding to each destination.  The interface between my Javascript/HTML front-end and the Rails back end was the Fetch API.  

The fetch() method is used to make asynchronous network requests to a database or a web server. If we were to only use synchronous methods, our program would be stuck waiting for that request to complete. The user may experience the screen "freezing". Performance may be slower. 

Since the fetch() method is asynchronous, we can hand off a long-running task to a thread, while the main program continues to execute.  We can manipulate the screen and entertain the user with messages or animation while the data is being processed in the background making for a better user experience and overall better performance.

This fetch() method returns a “Promise” object.  A “Promise” is an object that holds a value that is promised to be given to you at a later time.  A promise starts out in the pending state.  If the network request is successful,  it will change to the resolved state, or if an error occurs, it will be in the rejected state. (The success or error state relates to the network request itself, not the underlying operation.) Upon success, the promise returned by the fetch method will hold a response object that contains the data returned from that request.  Once the fetch request is completed, we can call the promises “then” method passing in an arrow function with that data parameter to access and process the data. We can chain the “then” and “catch” calls (which also return ‘Promise’ objects). 

In my code below to create a new destination, I call the fetch() method to send my “POST” request to add a destination to the database.  I have chained “.then” calls to first convert the data to parse the response to JSON and second use the data to render it to the page. I also have chained a “.catch” call to handle errors.  I have code after the fetch() call to clear the destination details section of my page which may have details of a previously viewed destination. This will execute concurrently with the fetch. 


```
function createDestination () {
    
    let inputDest = {
      name: document.getElementById('name').value,
      country: document.getElementById('country').value,
      currency: document.getElementById('currency').value,
      language: document.getElementById('language').value
    }
    fetch(DESTINATIONS_URL,{
        method: "POST",
        body: JSON.stringify(inputDest),
        headers: {
            'Content-Type': 'application/json',
            'Accept': 'application/json'
        }
    })
    .then(resp => resp.json())
    .then(dest => {
      let newDest = new Destination(dest);
      //add new destination to page
      newDest.renderDest();
      
      //Clear the input form and make it invisible
      let frmWrapper = document.getElementById("dest-form-container");
      frmWrapper.innerHTML = "";
      frmWrapper.style.display = 'none';
    })
    .catch((error) => {
      alert(`${error} on Creating New Destination` )
    }); 

    //clear right side of the page that still may have previously viewed has attractions
    let dstDetails = document.querySelector(".dest-details p");
    let dstBtnsCont = document.getElementById("dest-btns-container");
    let attrListDiv = document.querySelector(".attr-list ul");
    dstDetails.innerHTML = ""
    dstBtnsCont.innerHTML = ""
    attrListDiv.innerHTML = ''
  }
```

 In applications that deals with a large amount of data, executing tasks independent of the fetch() would make a noticeable improvement in performance. By using "Promises", we can improve performance and therby the user experience.  Indeed an ounce of performance is worth a pound of promises.
