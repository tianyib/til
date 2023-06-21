## Wait until all jQuery Ajax requests are done

```javascript
$.when(ajax1(), ajax2(), ajax3(), ajax4()).done(function(a1, a2, a3, a4){
    // will be executed when all four ajax requests are done.
    // a1, a2, a3 and a4 are lists containing the response text, status, and jqXHR object for each ajax calls.
});

function ajax1() {
    // must return the value from calling the $.ajax() method
    return $.ajax({
        url: "anyUrl",
        dataType: "json",
        data:  anyJsonData,            
        ...
    });
}
```
