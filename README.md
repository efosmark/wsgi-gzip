wsgi-gzip
=========

Simple WSGI middleware for automatic gzipping.

A WSGI middleware application that automatically gzips output to the client. Before doing any gzipping, it first checks the environ to see if the client can even support gzipped output. If not, it immediately drops out. It automatically modifies the headers to include the proper values for the 'Accept-Encoding' and 'Vary' headers. 

Example
-------

	from wsgiref.simple_server import WSGIServer, WSGIRequestHandler
	from gzipmiddleware import Gzipper
	
	def test_app(environ, start_response):
	    status = '200 OK'
	    headers = [('content-type', 'text/html')]
	    start_response(status, headers)

	    return ['Hello gzipped world!']

	app = Gzipper(test_app, compresslevel=8)
	httpd = WSGIServer(('', 8080), WSGIRequestHandler)
	httpd.set_app(app)
	httpd.serve_forever()
 
Author
------
Evan Fosmark -- This was originally published on my blog (25th December 2008), but I've since refacored that website and moved all of the code to this git repo.