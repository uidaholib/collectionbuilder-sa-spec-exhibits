# Long Range Campus Development Plans

These files were transferred from Brian Kelley as Web Technician for the Division of Finance and Administration in May 2021.
They come from a page on Facilities Services that they want to remove and would like to see as a library digital collection instead.

Original pages:

- https://www.uidaho.edu/infrastructure/facilities/aes/campus-development-plan
- https://www.uidaho.edu/infrastructure/facilities/aes/campus-development-plan/illustrative-plan
- https://www.uidaho.edu/infrastructure/facilities/aes/campus-development-plan/history

Archive versions:

- https://perma.cc/3UGY-HUN4
- https://perma.cc/EZ3M-GRWA
- https://perma.cc/GXV6-S95P

The PDF plans are generated from an AutoCAD drawing.

The images are simply taken from the website.
Ann  Ulliman (CADD Center Manager, AES/Facilities) reported that she was unable "to find the images located in the Facilities Archive so am unaware of where the originals are, or if we even still have them".


# collectionbuilder-sa-spec-exhibits

A customized version of CollectionBuilder-SA used to build standalone exhibit sites for University of Idaho SPEC.

- uiblackhistory
- hiroshima
- 1918flu

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
