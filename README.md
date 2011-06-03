# ePub Creator #

ePub Creator is a Django app originally written by Corey Oordt from the Washington Times. This fork is a maintained update of that app, for use with the Pandamian code base.

## What's Different? ##

A couple of things:

* Updated template encoding to 'UTF-8', as per EPUB2.01 specs
* Updated epubcheck to 1.2
* Fixed an issue for when an author has only one name
* Fixed an issue for handling of entity conversion
* Added a templates section to docs
* Reorganized documentation so you won't need to use Sphinx to build 


## Detailed Documentation ##

Corey has provided comprehensive documentation with the original version of ePub Creator. I've done some reorganization: the generated html docs are in documentation/; the Sphinx build files are available in docs_source/. (This way if you're lazy you won't have to install Sphinx to build documentation)

I've also added a section on Templates, which Corey left blank.

## Example ##

Generating an ePub with ePub creator is fairly simple. Here's an example taken from Pandamian:

```python
from appname.epub.models import EPub

final_path = os.path.join(temp_dir, "book.epub") 
e = EPub()

e.metadata.title = bookObj.title
e.metadata.add_creator(bookObj.author.first_name)
e.metadata.description = bookObj.description
e.metadata.publisher = 'Pandamian'
e.metadata.language = 'en'

#images, to be added later
#e.add_image(img_path, name='logo.svg')

s = Entry.objects.filter(book=bookObj, status=1)
for entry in s:
    e.add_entry(entry.title, entry, entry.slug+".html")
    
e.generate_epub(final_path)
```

Just drop the epub/ folder into your Django app, and remember to add it to your INSTALLED_APPS as 'yourappname.epub'. 


