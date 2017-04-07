# api documentation for  [phantomcss (v1.1.5)](https://github.com/Huddle/PhantomCSS#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-phantomcss.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-phantomcss) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-phantomcss.svg)](https://travis-ci.org/npmdoc/node-npmdoc-phantomcss)
#### A CasperJS module for automating visual regression testing of Web apps, live style guides and responsive layouts.

[![NPM](https://nodei.co/npm/phantomcss.png?downloads=true)](https://www.npmjs.com/package/phantomcss)

[![apidoc](https://npmdoc.github.io/node-npmdoc-phantomcss/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-phantomcss_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-phantomcss/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-phantomcss/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-phantomcss/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "James Cryer / Huddle"
    },
    "bugs": {
        "url": "https://github.com/Huddle/PhantomCSS/issues"
    },
    "dependencies": {
        "casperjs": "^1.1.2",
        "phantomjs-prebuilt": "^2.1.4",
        "resemblejs": "^2.2.2"
    },
    "description": "A CasperJS module for automating visual regression testing of Web apps, live style guides and responsive layouts.",
    "devDependencies": {},
    "directories": {},
    "dist": {
        "shasum": "bbceee88aef02c9ce8af91db22a37c04ea60627e",
        "tarball": "https://registry.npmjs.org/phantomcss/-/phantomcss-1.1.5.tgz"
    },
    "gitHead": "6b96c9ee44762097bad017f7e62ecf9009285ca0",
    "homepage": "https://github.com/Huddle/PhantomCSS#readme",
    "keywords": [
        "css",
        "phantomjs",
        "casperjs",
        "testing",
        "visual regression",
        "responsive"
    ],
    "license": "MIT",
    "main": "phantomcss.js",
    "maintainers": [
        {
            "name": "jamescryer",
            "email": "james.cryer@huddle.com"
        }
    ],
    "name": "phantomcss",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/Huddle/PhantomCSS.git"
    },
    "scripts": {},
    "version": "1.1.5"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module phantomcss](#apidoc.module.phantomcss)
1.  [function <span class="apidocSignatureSpan">phantomcss.</span>compareAll ( exclude, diffList, include )](#apidoc.element.phantomcss.compareAll)
1.  [function <span class="apidocSignatureSpan">phantomcss.</span>compareExplicit ( list )](#apidoc.element.phantomcss.compareExplicit)
1.  [function <span class="apidocSignatureSpan">phantomcss.</span>compareFiles ( baseFile, file )](#apidoc.element.phantomcss.compareFiles)
1.  [function <span class="apidocSignatureSpan">phantomcss.</span>compareMatched ( match, exclude )](#apidoc.element.phantomcss.compareMatched)
1.  [function <span class="apidocSignatureSpan">phantomcss.</span>compareSession ( list )](#apidoc.element.phantomcss.compareSession)
1.  [function <span class="apidocSignatureSpan">phantomcss.</span>done ()](#apidoc.element.phantomcss.done)
1.  [function <span class="apidocSignatureSpan">phantomcss.</span>getCreatedDiffFiles ()](#apidoc.element.phantomcss.getCreatedDiffFiles)
1.  [function <span class="apidocSignatureSpan">phantomcss.</span>getExitStatus ()](#apidoc.element.phantomcss.getExitStatus)
1.  [function <span class="apidocSignatureSpan">phantomcss.</span>init ( options )](#apidoc.element.phantomcss.init)
1.  [function <span class="apidocSignatureSpan">phantomcss.</span>screenshot ( target, timeToWait, hideSelector, fileName )](#apidoc.element.phantomcss.screenshot)
1.  [function <span class="apidocSignatureSpan">phantomcss.</span>turnOffAnimations ()](#apidoc.element.phantomcss.turnOffAnimations)
1.  [function <span class="apidocSignatureSpan">phantomcss.</span>update ( options )](#apidoc.element.phantomcss.update)
1.  [function <span class="apidocSignatureSpan">phantomcss.</span>waitForTests ( tests )](#apidoc.element.phantomcss.waitForTests)



# <a name="apidoc.module.phantomcss"></a>[module phantomcss](#apidoc.module.phantomcss)

#### <a name="apidoc.element.phantomcss.compareAll"></a>[function <span class="apidocSignatureSpan">phantomcss.</span>compareAll ( exclude, diffList, include )](#apidoc.element.phantomcss.compareAll)
- description and source-code
```javascript
function compareAll( exclude, diffList, include ) {
	var tests = [];

	if ( !diffList ) {
		diffList = getDiffs( _results );
		if(exclude || include){
			diffList = diffList.filter(filterOn( str2RegExp(include), str2RegExp(exclude) ));
		}
		//diffList.forEach(function(path){console.log( '[PhantomCSS] Attempting visual comparison of ' + path );})
	}

	diffList.forEach( function ( file ) {
		var baseFile = _replaceDiffSuffix( file );
		tests.push( compareFiles( baseFile, file ) );
	} );

	waitForTests( tests );
}
```
- example usage
```shell
...

### Compare the images when and how you want

'''javascript
/*
	String is converted into a Regular expression that matches on full image path
*/
phantomcss.compareAll('exclude.test');

// phantomcss.compareMatched('include.test', 'exclude.test');
// phantomcss.compareMatched( new RegExp('include.test'), new RegExp('exclude.test'));

/*
	Compare image diffs generated in this test run only
*/
...
```

#### <a name="apidoc.element.phantomcss.compareExplicit"></a>[function <span class="apidocSignatureSpan">phantomcss.</span>compareExplicit ( list )](#apidoc.element.phantomcss.compareExplicit)
- description and source-code
```javascript
function compareExplicit( list ) {
	// An explicit list of diff images to compare ['/dialog.diff.png', '/header.diff.png']
	compareAll( void 0, list );
}
```
- example usage
```shell
...
	Compare image diffs generated in this test run only
*/
// phantomcss.compareSession();

/*
	Explicitly define what files you want to compare
*/
// phantomcss.compareExplicit(['/dialog.diff.png', '/header.diff.png']);

/*
	Get a list of image diffs generated in this test run
*/
// phantomcss.getCreatedDiffFiles();

/*
...
```

#### <a name="apidoc.element.phantomcss.compareFiles"></a>[function <span class="apidocSignatureSpan">phantomcss.</span>compareFiles ( baseFile, file )](#apidoc.element.phantomcss.compareFiles)
- description and source-code
```javascript
function compareFiles( baseFile, file ) {
	var test = {
		filename: baseFile
	};

	if ( !_isFile( baseFile ) ) {
		test.error = true;
	} else {

		casper.thenOpen( 'about:blank', function () {}); // reset page (fixes bug where failure screenshots leak between captures)
		casper.thenOpen( 'file:///' + _resembleContainerPath, function () {

			asyncCompare( baseFile, file, function ( isSame, mismatch ) {

				if ( !isSame ) {

					test.fail = true;

					casper.waitFor(
						function check() {
							return casper.evaluate( function () {
								return window._imagediff_.hasImage;
							} );
						},
						function () {
							var failFile, safeFileName, increment;

							if ( _failures ) {
								// flattened structure for failed diffs so that it is easier to preview
								failFile = _failures + fs.separator + file.split( /\/|\\/g ).pop().replace( _diffImageSuffix + '.png', '' ).replace( '.png
', '' );
								safeFileName = failFile;
								increment = 0;

								while ( _isFile( safeFileName + _failureImageSuffix + '.png' ) ) {
									increment++;
									safeFileName = failFile + '.' + increment;
								}

								failFile = safeFileName + _failureImageSuffix + '.png';
								casper.captureSelector( failFile, 'img' );

								test.failFile = failFile;
							}

							if ( file.indexOf( _diffImageSuffix + '.png' ) !== -1 ) {
								casper.captureSelector( file.replace( _diffImageSuffix + '.png', _failureImageSuffix + '.png' ), 'img' );
							} else {
								casper.captureSelector( file.replace( '.png', _failureImageSuffix + '.png' ), 'img' );
							}

							casper.evaluate( function () {
								window._imagediff_.hasImage = false;
							} );

							if ( mismatch ) {
								test.mismatch = mismatch;
								_onFail( test ); // casper.test.fail throws and error, this function call is aborted
								return; // Just to make it clear what is happening
							} else {
								_onTimeout( test );
							}

						},
						function () {},
						_waitTimeout
					);
				} else {
					test.success = true;
					_onPass( test );
				}

			} );
		} );
	}
	return test;
}
```
- example usage
```shell
...
	Get a list of image diffs generated in this test run
*/
// phantomcss.getCreatedDiffFiles();

/*
	Compare any two images, and wait for the results to complete
*/
// phantomcss.compareFiles(baseFile, diffFile);
// phantomcss.waitForTests();

'''

### Best Practices

##### Name your screenshots!
...
```

#### <a name="apidoc.element.phantomcss.compareMatched"></a>[function <span class="apidocSignatureSpan">phantomcss.</span>compareMatched ( match, exclude )](#apidoc.element.phantomcss.compareMatched)
- description and source-code
```javascript
function compareMatched( match, exclude ) {
	// Search for diff images, but only compare matched filenames
	compareAll( exclude, void 0, match);
}
```
- example usage
```shell
...

'''javascript
/*
	String is converted into a Regular expression that matches on full image path
*/
phantomcss.compareAll('exclude.test');

// phantomcss.compareMatched('include.test', 'exclude.test');
// phantomcss.compareMatched( new RegExp('include.test'), new RegExp('exclude.test'));

/*
	Compare image diffs generated in this test run only
*/
// phantomcss.compareSession();
...
```

#### <a name="apidoc.element.phantomcss.compareSession"></a>[function <span class="apidocSignatureSpan">phantomcss.</span>compareSession ( list )](#apidoc.element.phantomcss.compareSession)
- description and source-code
```javascript
function compareSession( list ) {
	// compare the diffs created in this session
	compareAll( void 0, getCreatedDiffFiles() );
}
```
- example usage
```shell
...

// phantomcss.compareMatched('include.test', 'exclude.test');
// phantomcss.compareMatched( new RegExp('include.test'), new RegExp('exclude.test'));

/*
	Compare image diffs generated in this test run only
*/
// phantomcss.compareSession();

/*
	Explicitly define what files you want to compare
*/
// phantomcss.compareExplicit(['/dialog.diff.png', '/header.diff.png']);

/*
...
```

#### <a name="apidoc.element.phantomcss.done"></a>[function <span class="apidocSignatureSpan">phantomcss.</span>done ()](#apidoc.element.phantomcss.done)
- description and source-code
```javascript
function done(){
	_count = 0;
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.phantomcss.getCreatedDiffFiles"></a>[function <span class="apidocSignatureSpan">phantomcss.</span>getCreatedDiffFiles ()](#apidoc.element.phantomcss.getCreatedDiffFiles)
- description and source-code
```javascript
function getCreatedDiffFiles() {
	var d = diffsCreated;
	diffsCreated = [];
	return d;
}
```
- example usage
```shell
...
	Explicitly define what files you want to compare
*/
// phantomcss.compareExplicit(['/dialog.diff.png', '/header.diff.png']);

/*
	Get a list of image diffs generated in this test run
*/
// phantomcss.getCreatedDiffFiles();

/*
	Compare any two images, and wait for the results to complete
*/
// phantomcss.compareFiles(baseFile, diffFile);
// phantomcss.waitForTests();
...
```

#### <a name="apidoc.element.phantomcss.getExitStatus"></a>[function <span class="apidocSignatureSpan">phantomcss.</span>getExitStatus ()](#apidoc.element.phantomcss.getExitStatus)
- description and source-code
```javascript
function getExitStatus() {
	return exitStatus;
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.phantomcss.init"></a>[function <span class="apidocSignatureSpan">phantomcss.</span>init ( options )](#apidoc.element.phantomcss.init)
- description and source-code
```javascript
function init( options ) {
	update( options );
}
```
- example usage
```shell
...
* 'casperjs test demo/testsuite.js --engine=slimerjs'

### Options and setup

If you are using SlimerJS, you will need to specify absolute paths (see 'demo').

'''javascript
phantomcss.init({

/*
captureWaitEnabled defaults to true, setting to false will remove a small wait/delay on each
screenshot capture - useful when you don't need to worry about
animations and latency in your visual tests
*/
captureWaitEnabled: true,
...
```

#### <a name="apidoc.element.phantomcss.screenshot"></a>[function <span class="apidocSignatureSpan">phantomcss.</span>screenshot ( target, timeToWait, hideSelector, fileName )](#apidoc.element.phantomcss.screenshot)
- description and source-code
```javascript
function screenshot( target, timeToWait, hideSelector, fileName ) {
	var name;

	if ( isComponentsConfig( target ) ) {
		for ( name in target ) {
			if ( isComponentsConfig( target[ name ] ) ) {
				waitAndHideToCapture( target[ name ].selector, name, target[ name ].ignore, target[ name ].wait );
			} else {
				waitAndHideToCapture( target[ name ], name );
			}
		}
	} else {
		if ( isNaN( Number( timeToWait ) ) && ( typeof timeToWait === 'string' ) ) {
			fileName = timeToWait;
			timeToWait = void 0;
		}
		waitAndHideToCapture( target, fileName, hideSelector, timeToWait );
	}
}
```
- example usage
```shell
...
	start( url ).
	then(function(){
		
		// do something
		casper.click('button#open-dialog');
		
		// Take a screenshot of the UI component
		phantomcss.screenshot('#the-dialog', 'a screenshot of my dialog');

	});
'''

From the command line/terminal run:

* 'casperjs test demo/testsuite.js'
...
```

#### <a name="apidoc.element.phantomcss.turnOffAnimations"></a>[function <span class="apidocSignatureSpan">phantomcss.</span>turnOffAnimations ()](#apidoc.element.phantomcss.turnOffAnimations)
- description and source-code
```javascript
function turnOffAnimations() {
	console.log( '[PhantomCSS] Turning off animations' );
	casper.evaluate( function turnOffAnimations() {

		function disableAnimations() {
			var jQuery = window.jQuery;
			if ( jQuery ) {
				jQuery.fx.off = true;
			}

			var css = document.createElement( "style" );
			css.type = "text/css";
			css.innerHTML = "* { -webkit-transition: none !important; transition: none !important; -webkit-animation: none !important; animation
: none !important; }";
			document.body.appendChild( css );
		}

		if ( document.readyState !== "loading" ) {
			disableAnimations();
		} else {
			window.addEventListener( 'load', disableAnimations, false );
		}
	} );
}
```
- example usage
```shell
...
	*/
	rebase: casper.cli.get("rebase")
});

/*
	Turn off CSS transitions and jQuery animations
*/
phantomcss.turnOffAnimations();
'''

### Don't like pink?

![A failed visual regression test, yellow areas show where the icon has enlarged and pushed other elements down.](https://raw.github
.com/Huddle/PhantomCSS/master/readme_assets/differentcolour.png "Failed visual regression test")

'''javascript
...
```

#### <a name="apidoc.element.phantomcss.update"></a>[function <span class="apidocSignatureSpan">phantomcss.</span>update ( options )](#apidoc.element.phantomcss.update)
- description and source-code
```javascript
function update( options ) {

	function stripslash( str ) {
		return ( str || '' ).replace( /\/\//g, '/' ).replace( /\\/g, '\\' );
	}

	options = options || {};

	casper = options.casper || casper;

	_waitTimeout = options.waitTimeout || _waitTimeout;

	_libraryRoot = options.libraryRoot;

	_resemblePath = _resemblePath || getResemblePath( _libraryRoot );

	_resembleContainerPath = _resembleContainerPath || getResembleContainerPath( _libraryRoot );

	_src = stripslash( options.screenshotRoot || _src );
	_results = stripslash( options.comparisonResultRoot || options.screenshotRoot || _results || _src );
	_failures = options.failedComparisonsRoot === false ? false : stripslash( options.failedComparisonsRoot || _failures );

	_fileNameGetter = options.fileNameGetter || _fileNameGetter;

	_prefixCount = options.prefixCount || _prefixCount;
	_isCount = ( options.addIteratorToImage !== false );

	_onPass = options.onPass || _onPass;
	_onFail = options.onFail || _onFail;
	_onTimeout = options.onTimeout || _onTimeout;
	_onNewImage = options.onNewImage || _onNewImage;
	_onComplete = options.onComplete || options.report || _onComplete;

	_hideElements = options.hideElements;

	_mismatchTolerance = options.mismatchTolerance || _mismatchTolerance;

	_rebase = isNotUndefined(options.rebase) ? options.rebase : _rebase;

	_resembleOutputSettings = options.outputSettings || _resembleOutputSettings;

	_resembleOutputSettings.useCrossOrigin=false; // turn off x-origin attr in Resemble to support SlimerJS

	_cleanupComparisonImages = options.cleanupComparisonImages || _cleanupComparisonImages;

	_baselineImageSuffix = options.baselineImageSuffix || _baselineImageSuffix;
	_diffImageSuffix = options.diffImageSuffix || _diffImageSuffix;
	_failureImageSuffix = options.failureImageSuffix || _failureImageSuffix;

	_captureWaitEnabled = isNotUndefined(options.captureWaitEnabled) ? options.captureWaitEnabled : _captureWaitEnabled;

	if ( options.addLabelToFailedImage !== undefined ) {
		_addLabelToFailedImage = options.addLabelToFailedImage;
	}

	if ( _cleanupComparisonImages ) {
		_results += fs.separator + generateRandomString();
	}
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.phantomcss.waitForTests"></a>[function <span class="apidocSignatureSpan">phantomcss.</span>waitForTests ( tests )](#apidoc.element.phantomcss.waitForTests)
- description and source-code
```javascript
function waitForTests( tests ) {
	casper.then( function () {
		casper.waitFor( function () {
				return tests.length === tests.reduce( function ( count, test ) {
					if ( test.success || test.fail || test.error ) {
						return count + 1;
					} else {
						return count;
					}
				}, 0 );
			}, function () {
				var fails = 0,
					errors = 0;
				tests.forEach( function ( test ) {
					if ( test.fail ) {
						fails++;
					} else if ( test.error ) {
						errors++;
					}
				} );
				_onComplete( tests, fails, errors );
			}, function () {

			},
			_waitTimeout );
	} );
}
```
- example usage
```shell
...
*/
// phantomcss.getCreatedDiffFiles();

/*
	Compare any two images, and wait for the results to complete
*/
// phantomcss.compareFiles(baseFile, diffFile);
// phantomcss.waitForTests();

'''

### Best Practices

##### Name your screenshots!
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
