JsonNetMediaTypeFormatter
=========================

A MediaTypeFormatter for use with ASP.NET Web API to ensure (de)serialization of derived classes through the wire.

### The problem

ASP.NET Web API uses JSON.net to (de)serialize objects in JSON syntax, and it performs well for most use cases.

However, out of the box, the default (de)serialization pattern in use is not able to convert JSON notation back to a derived class if the Web API action is expecting a parent class. 

For example:

``` csharp

class Parent { }
class Child : Parent { }


// in the controller

public void Post (Parent entity) {

    // [entity] will always be of type Parent, even if we sent in an object of type Child

}

```

This behavior is consistent, even if the JSON string contains type information generated by JSON.net.

`JsonNetMediaTypeFormatter` is meant to replace the default `JsonMediaTypeFormatter` that Web API uses out of the box to help remedy this use case.