# Functions all the way down

browser (url, ..., doneLoading) {
	var request = new HttpRequest()
	request.url = url
	request.headers = ...
	
	server(request, function (response) {
		doneLoading(new Document(response))
	})
}

# State
Just long-lived arguments, Side effect

# Router
Simply an advanced switch statement.
Calling a function is dispatching it. Dynamic dispatch / multiple dispatch is when the same function calls different underlying implementations depending on the input.

A router returns a dispatcher. See the point?

# HTML
HTML is just a DSL for the DOM. Likewise, CSS is just a DSL for the CSSOM