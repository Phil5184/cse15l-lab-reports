## StringServer Code
![Image](Labreport2code.jpg)

##  First Screenshot of using `/add-message`
![Image](Labreport2screenshot.jpg)
The method in my code that was called was the `handleRequest` method (The main method inside of the `StringServer` class was obviously called as well when the server started). The relevant fields inside the `Handler` class was a `String` variable that I named `ss1`, which was the string that would be continuously added onto and shown on the web server. There was also a `int` `z` variable that tracked the number of the lines of the string shown in the web server, as well as the `URI` `url` field that stores the url of the web server. The `ss1` `String` variable initially stored just a empty `String`, but after the request was called, it then stored the `String "1. hello"`. The `int` `z` variable was also updated to `2` to track the next line number, and the `URI` `url` field was updated to have the path and query `/add-message?s=hello`.

## Second Screenshot of Using `/add-message`
![Image](Labreport2screenshot2.jpg)
The method in my code that was called was the `handleRequest` method. The relevant fields inside the `Handler` class was a `String` variable that I named `ss1`, which was the string that would be continuously added onto and shown on the web server. There was also a `int` `z` variable that tracked the number of the lines of the string shown in the web server, as well as the `URI` `url` field that stores the url of the web server. The `ss1` `String` variable initially stored `"1. hello"` before the request above was called, but after the request was called, it then stored the `String` `"1. hello \n 2. how are you"`. The `int` `z` variable was also updated to `3` to track the next line number, and the `URI` `url` field was updated to have the path and query `/add-message?s=how are you`.

