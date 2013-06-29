
# Edit the LIBRARY_FILES list to determine what libraries are
# compiled into lib.js and included on the page

LIBRARY_FILES =	\
	build/jquery.js \
	build/underscore.js \
	build/d3.js \
	build/handlebars.runtime.js

# To add more files to your lib, add them up above like this.
# No trailing slash needed on the last line.
#	build/queue.js \
#	build/d3.js \
#	build/ink.js \
#	build/tablespoon.js \ 

GENERATED_FILES = \
	js/lib.js
	
# public/_assets/templates.js

all: $(GENERATED_FILES)

clean:
	rm -rf -- $(GENERATED_FILES) build

.SECONDARY:

css/lib.css: css/bootstrap-responsive.min.css css/bootstrap.min.css
	cat $^ >$@

build/jquery.js:
	mkdir -p build
	curl --raw -o $@ 'http://code.jquery.com/jquery-2.0.0.min.js'

build/underscore.js:
	mkdir -p build
	curl --raw -o $@ 'http://underscorejs.org/underscore.js'

build/d3.js:
	mkdir -p build
	curl --raw -o $@ 'http://d3js.org/d3.v3.js'

build/queue.js:
	mkdir -p build
	curl --raw -o $@ 'http://d3js.org/queue.v1.js'

build/handlebars.runtime.js:
	mkdir -p build
	curl --raw -o $@ 'https://raw.github.com/wycats/handlebars.js/1.0.0-rc.4/dist/handlebars.runtime.js'

js/lib.js: $(LIBRARY_FILES)
	node_modules/.bin/uglifyjs $^ -c -m -o $@

public/_assets/templates/*.ejs:
	mkdir -p public/_assets/templates

public/_assets/templates/*.hbs:
	mkdir -p public/_assets/templates

public/_assets/templates.js: public/_assets/templates/*.ejs public/_assets/templates/*.hbs
	echo "Compiling client-size templates from public/_assets/templates"
	./bin/compile-templates.js > $@ 

.PHONY: index

index:
	./render.js