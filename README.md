# collectionbuilder-sa-spec-exhibits

Offensive Content Flag: 

"Materials in this collection may contain images, language, or other content that may be offensive or disturbing. These materials are a product of a time and place in history and should be viewed within their historical context. To maintain historical accuracy, the materials appear as they were originally created to serve as historical evidence of the social mindsets, occurrences, behaviors, and norms of their time. They do not reflect the current views of the University of Idaho. For more information on how we treat archival materials with offensive or disturbing content, please see the University of Idaho Library, Special Collections and Archives Offensive Content Policy."

A customized version of CollectionBuilder-SA used to build standalone exhibit sites for University of Idaho SPEC.

- uiblackhistory
- hiroshima
- 1918flu
- ernieday
- lrcdp

Objects workflow:

- digital objects are stored on Webpages drive, in Webpages > library > spec > objects, in a folder matching the collection stub name. 
    - E.g. uiblackhistory, will be in S:Webpages\library\spec\objects\uiblackhistory , which will be on web at https://webpages.uidaho.edu/library/spec/objects/uiblackhistory
- the web location of the digital objects must be set in "_config.yml", in the `objects` option using the full url to their location
    - E.g. `objects: https://webpages.uidaho.edu/library/spec/objects/hiroshima`
- digital objects should not be committed to the repository ("objects" is gitignored). However, you can add objects on your local machine to test and/or generate derivatives.
- to process objects with Rake task:
    - add new items to folder "objects/archives"
    - run `rake generate_derivatives`
    - the task will check "objects/archives", then copy files to "objects/", and generate derivatives in "objects/small/" and "objects/thumbs/"
    - this folder structure can be copied over to the Webpages shared drive into the appropriate folder (e.g. S:Webpages\library\spec\objects\uiblackhistory )
    - once copied over, the template will work (using the live web images) locally or on the live web
- to test locally (without moving things to Webpages)
    - process objects with Rake as above
    - change config `objects` value to `objects: /objects`
    - when you `jekyll s` it will load images from the local objects folder rather than Webpages.

**Important filename notes:** 
The Rake task downcases all filenames and extensions to avoid issues on the web. 
It is best to start by creating all lowercase filenames, with no spaces, no odd characters (other than `-` or `_`), and no periods (`.` other than the extension).
If you didn't start with lowercase filenames, be sure to downcase your metadata `filename` column.
Also, please ensure filenames are unique *without* the extension (e.g. avoid using both `ex1.jpg` and `ex1.pdf`), since CB won't be able to produce separate derivatives.
