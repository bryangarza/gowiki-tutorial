Writing Web Applications @ http://golang.org/doc/articles/wiki/
===============================================================

`> BRAINDUMP EXECUTE`

Flow of the application so far, we listen at port 8080 using
http.ListenAndServe, push that to the handler func (http.HandleFunc, obvi.) and
then we write to our `w` of type `http.ResponseWriter` an HTML formatted
string (in func ViewHandler()).

We're handling from `/view/` so we later chop that off in viewHandler.

we're taking all the requests to `/view/` and handling them with the function
ViewHandler()

d'oh! had test.txt typo-ed as text.txt, so I was getting a nil pointer error :0

I'm already at the `Saving Pages` section
(http://golang.org/doc/articles/wiki/#tmp_8)
and it seems like newlines aren't preserved when saving. Also, we keep
repeating the part of code that extracts the title:
```go
title := r.URL.Path[len("/save/"):]
```
for example, is the same for `/edit/` and `/view/`.

http.Error() replies to the request (in this case `w`), just like the other
http.ResponseWriter does when there are no errors.

from http://golang.org/doc/articles/wiki/#tmp_10 Template Caching
```
The function template.Must is a convenience wrapper that panics when passed a
non-nil error value, and otherwise returns the *Template unaltered. A panic is
appropriate here; if the templates can't be loaded the only sensible thing to
do is exit the program.

The ParseFiles function takes any number of string arguments that identify our
template files, and parses those files into templates that are named after the
base file name. If we were to add more templates to our program, we would add
their names to the ParseFiles call's arguments.
```

Now we've abstracted getting the title using getTitle() and added validation so
we can't go to an arbitrary path.
