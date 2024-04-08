# jdgallery
JDGallery is a small Python script generating a number of HTML files from jpeg images that make up a image gallery to browse with any html browser. Inspired by [BBGallery](https://bbgallery.sourceforge.net/)

BBGallery was the first tool I ever encountered that counted as *Infrastructure as Code*. It built customizable
file-based image galleries from scratch. It seems to be a dead project; I want to re-create it.

Apparently BBGallery was written by (and named afte) Bodo Bauer. 

When you ran `bbgallery` in a folder full of images, it would set about to create thumbnail versions of those 
images, followed by creating uniformly scaled versions of them, as well. Then it created an HTML page for 
each scaled image. In that page, wHen you clicked on the scaled image, it would let you directly view /download 
the original image. Each scaled HTML page had a link forwards and backwards to the scaled HTML pages for the 
next and previous scaled images, alphabetically by file name. It also created index HTML pages, each containing 
the thumbnail imaged, linked to the appropriate scaled HTML page that corresponds to the thumbnail image. 

You could control the size of the thumbnails, the size of the scaled images, and how many thumbnails would 
appear on each of index pages (it would create nough indexes for all the image thumbnails, with corresponding 
forward and backwards links on each index, as well.)

I appreciated the primary design goal (as I understood it) of BBGallery, which is that it created a way to look
at pictures that did not require a tremendous infrastrcucture to operate or maintaing the gallery. It statically created all the files needed for a reasonably useful (at the time) gallery. 

It operated at the file system level, meaning you could make a directory full of images, run `bbgallery` in it, 
and that directory became a web-based image gallery that you could tar/compress and move to another server, you 
could open the files locally with a browser, you could burn it to a CD-ROM (yeah that was a thing, once). It 
didn't require a particular web server with particular modules or configuration--just one that did basic HTTP. 
It created thumb nails and "web optimized" copies of your photos, but also left you photos intact for archival 
purposes.

Another part of that design I appreciate was that, the first time you created a gallery in an image directory, 
it would create a dot file in the directory, and write the called configuration information there. That is, when
you ran `bbgallery`, you may have told it how big to make the thumbnails and scaled images, how many thumbnails 
to put on each index page, what to call the gallery,etc. It would record all those command-line flags that you 
provided at initial creation into the dotfile. Then, if/when you want add or remove images to that directory, 
you only had to run `bbgallery` again, all by itself. It would figure out what commands line options were used 
previously, and re-use them, updating the gallery with the new or removed images. I would take advantage of this 
in various cron-jobs or even when using `inotifywait` to detect image file changes and automatically update 
my galleries.

I intend to re-implement most if not all of these functions. Currently, I do not commit to using the same 
command-line syntax or having the exact same run time behaviors, but that might change depending on how I feel.

Improvements I intend to make are:

 o Support JPG, PNG, GIF, and SVG file types
   o To make this harder, also try to only use Python libraries that can be installed via `pip`, no shelling out directly to ImageMagick or Gimp
 o Support pulling metadata out of the files to make availabe in the gallery view
 o Support a more modern dynamic mobile friendly UI that allows flipping through images
   o Note that I hate writing javascript, I hate the DOM model for programming, and I hate having to learn and update third-party javascript libraries. So no promises on this one.

Well, I actually used up all my time just writing this up--I didn't even get any skeleton code brought together. 
I'm not sure when I'll get more time and motiviation to get back to this.  Hopefully soon.
