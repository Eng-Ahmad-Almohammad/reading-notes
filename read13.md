# Table of content
 |Read No. | Name of chapter|
 |:---------: |:--------------:|
 |13|[Local Storage](https://eng-ahmad-almohammad.github.io/Local-Storage/)|








 # Local Storage

## INTRODUCING HTML5 STORAGE

### So what is HTML5 Storage? Simply put, it’s a way for web pages to store named key/value pairs locally, within the client web browser. Like cookies, this data persists even after you navigate away from the web site, close your browser tab, exit your browser, or what have you. Unlike cookies, this data is never transmitted to the remote web server (unless you go out of your way to send it manually). It is implemented natively in web browsers, so it is available even when third-party browser plugins are not.

### Which browsers? Well, the latest version of pretty much every browser supports HTML5 Storage… even Internet Explorer!
### From your JavaScript code, you’ll access HTML5 Storage through the localStorage object on the global window object. Before you can use it, you should detect whether the browser supports it.
![storeg](https://user-images.githubusercontent.com/70091044/93810408-49478680-fc57-11ea-8586-00800e5c5f24.PNG)

### Instead of writing this function yourself, you can use Modernizr to detect support for HTML5 Storage.

### if (Modernizr.localstorage) {
### // window.localStorage is available!
### } else {
###  // no native support for HTML5 storage :(
###  // maybe try dojox.storage or a third-party solution}



## USING HTML5 STORAGE

### HTML5 Storage is based on named key/value pairs. You store data based on a named key, then you can retrieve that data with the same key. The named key is a string. The data can be any type supported by JavaScript, including strings, Booleans, integers, or floats. However, the data is actually stored as a string. If you are storing and retrieving anything other than strings, you will need to use functions like parseInt() or parseFloat() to coerce your retrieved data into the expected JavaScript datatype.



## TRACKING CHANGES TO THE HTML5 STORAGE AREA


### If you want to keep track programmatically of when the storage area changes, you can trap the storage event. The storage event is fired on the window object whenever setItem(), removeItem(), or clear() is called and actually changes something. For example, if you set an item to its existing value or call clear() when there are no named keys, the storage event will not fire, because nothing actually changed in the storage area. The storage event is supported everywhere the localStorage object is supported, which includes Internet Explorer 8. IE 8 does not support the W3C standard addEventListener (although that will finally be added in IE 9). Therefore, to hook the storage event, you’ll need to check which event mechanism the browser supports. 

### if (window.addEventListener) {
### window.addEventListener("storage", handle_storage, false);
### } else {
###  window.attachEvent("onstorage", handle_storage);
### };
### The handle_storage callback function will be called with a StorageEvent object, except in Internet Explorer where the event object is stored in window.event.

### function handle_storage(e) {
###  if (!e) { e = window.event; }
### }
### At this point, the variable e will be a StorageEvent object, which has the following useful properties.
![storegevent object](https://user-images.githubusercontent.com/70091044/93809352-d689db80-fc55-11ea-80eb-7b7e2999a761.PNG)
## HTML5 STORAGE IN ACTION
### Let’s see HTML5 Storage in action. Recall the Halma game. There’s a small problem with the game: if you close the browser window mid-game, you’ll lose your progress. But with HTML5 Storage, we can save the progress locally, within the browser itself. Here is a live demonstration. Make a few moves, then close the browser tab, then re-open it. If your browser supports HTML5 Storage, the demonstration page should magically remember your exact position within the game, including the number of moves you’ve made, the position of each of the pieces on the board, and even whether a particular piece is selected.

### How does it work? Every time a change occurs within the game, we call this function:

### function saveGameState() {
###    if (!supportsLocalStorage()) { return false; }
###    localStorage["halma.game.in.progress"] = gGameInProgress;
###    for (var i = 0; i < kNumPieces; i++) {
###	localStorage["halma.piece." + i + ".row"] = gPieces[i].row;
###	localStorage["halma.piece." + i + ".column"] = gPieces[i].column;
###    }
###    localStorage["halma.selectedpiece"] = gSelectedPieceIndex;
###    localStorage["halma.selectedpiecehasmoved"] = gSelectedPieceHasMoved;
###    localStorage["halma.movecount"] = gMoveCount;
###    return true;
### }


## BEYOND NAMED KEY-VALUE PAIRS: COMPETING VISIONS
### While the past is littered with hacks and workarounds, the present condition of HTML5 Storage is surprisingly rosy. A new API has been standardized and implemented across all major browsers, platforms, and devices. As a web developer, that’s just not something you see every day, is it? But there is more to life than “5 megabytes of named key/value pairs,” and the future of persistent local storage is… how shall I put it… well, there are competing visions. One vision is an acronym that you probably know already: SQL. In 2007, Google launched Gears, an open source cross-browser plugin which included an embedded database based on SQLite. This early prototype later influenced the creation of the Web SQL Database specification. Web SQL Database (formerly known as “WebDB”) provides a thin wrapper around a SQL database, allowing you to do things like this from JavaScript:

![storeg html](https://user-images.githubusercontent.com/70091044/93810124-dfc77800-fc56-11ea-8e82-27e02bd5d200.PNG)