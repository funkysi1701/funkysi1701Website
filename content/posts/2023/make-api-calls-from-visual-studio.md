+++
title = "Make API calls from Visual Studio or Visual Studio Code"
date = "2023-11-16T00:00:00Z"
year = "2023"
month= "2023-11"
author = "funkysi1701"
authorTwitter = "funkysi1701" #do not include @
copyright = false
cover = "/images/monthly-costs.png"
images = ['/images/monthly-costs.png']
tags = ["Visual Studio", "API" ]
category="tech"
keywords = ["", ""]
description = "Make API calls from Visual Studio or Visual Studio Code"
summary = "Make API calls from Visual Studio or Visual Studio Code"
showFullContent = false
readingTime = true
draft = false
aliases = [
    "/2023/11/17/make-api-calls-from-visual-studio"
]
+++
It is that exciting time of year where Microsoft announce a new version of .Net (Version 8 this time) and Visual Studio. There have been lots of announcements which I am still digesting, but one that caught my eye was a new window in Visual Studio that shows all your API endpoints.

The new window is called **Endpoint Explorer** and can be added from the menu **View > Other Windows > Endpoint Explorer**.


If you right click on one of the endpoints you can view the code or send a request. It works with minimal APIs or standard MVC APIs. If you select send a request a .http file will be created, this is a feature that has been in Visual Studio for a while but I haven't taken much notice.

The syntax for writng these API calls is fairly simple

```
GET {{Catalog.API_HostAddress}}/api/v1/catalog/items
```

Or something more complex, this one is a POST with a body and a header. This is how you might call APIs which require authentication. Just include a header with your auth token.


```
POST {{Catalog.API_HostAddress}}/api/v1/catalog/items
Accept: application/json

{
    "name": "Test",
    "description": "Test",
    "price": 1.99,
    "pictureFileName": "test.png",
    "pictureUri": "https://picsum.photos/200/300"

}

```

You can also set up various variables at the top of your .http files by prefixing with an @, by default you get one that defines your base URL, but you can add more. 

eg @variable = value

Full docs of how you use .http files can be found [here](https://learn.microsoft.com/en-us/aspnet/core/test/http-files?view=aspnetcore-8.0) 

A hyperlink above each API call labelled Send request initiates the API call and your window splits in half with the right hand side displaying the response.

The response has four tabs, a nicely json formatted response, a raw response, a headers tab and a request tab.

Now you will notice an env box underneath your file tabs, where the method dropdown is in a normal c# class file. It took me a while to figure out how to setup environments, but you can add a file that contain environment specific config, like base URL for test/prod/dev etc.

This blog post tells me about it [here](https://devblogs.microsoft.com/visualstudio/safely-use-secrets-in-http-requests-in-visual-studio-2022/) but the name thing is add a json file called **http-client.env.json** and create some json like this:

```
  "local": {
    "ProjectPyramidApi_HostAddress": "http://localhost:44338"
  },
  "dev": {
    "ProjectPyramidApi_HostAddress": "https://dev.example.com"
  },
  "test": {
    "ProjectPyramidApi_HostAddress": "https://test.example.com"
  },
  "prod": {
    "ProjectPyramidApi_HostAddress": "https://prod.example.com"
  }
```

Other environment specific variables can be added in the same way.
