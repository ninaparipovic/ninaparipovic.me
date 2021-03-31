The crawler will run as follows:

1. start from a command line as shown in the User Interface
2. parse the command line, validate parameters, initialize other modules
3. fetch the webpage at `seedURL` and if it fails , take an appropriate action
4. store that webpage in a file in the `pageDirectory` with `documentID= 0`, with the contents as described in the User Interface above with
depth=0
5. add that page to the ***bag*** of webpages to crawl
6. add that URL to the ***hashtable*** of URLs seen
7. while there are more webpages to crawl,

	7.1 extract a webpage (URL,depth) item from the ***bag*** of webpages to be crawled
	7.2 **pause for at least one second**
	7.3 use *pagefetcher* to retrieve a webpage for that URL
	7.4 use *pagesaver* to write the webpage to the `pageDirectory` with a unique document ID, as described in the Requirements.
	7.5  if the webpage depth is < `maxDepth`, explore the webpage to find the links it contains:

                7.5.1 use *pagescanner* to parse the webpage to extract all its embedded URLs
	        7.5.2 for each extracted URL:

                	7.5.2.1. 'normalize' the URL (see below)
	               	7.5.2.2. if that URL is not 'internal' (see below), ignore it;
	               	7.5.2.3. try to insert that URL into the *hashtable* of URLs seen
	                7.5.2.4. if it was already in the table, do nothing;
	                7.5.2.5. if it was added to the table:

                                7.5.2.5.1. create a new *webpage* for that URL, at depth+1
	                        7.5.2.5.2. add that new *webpage* to the ***bag*** of webpages to be crawled
