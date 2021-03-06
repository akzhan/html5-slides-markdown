html5-slides-markdown
=====================

Generates a slideshow using the slides that power
[the html5-slides presentation](http://apirocks.com/html5/html5.html).

A `python` with the `jinja2` and `markdown` modules are required.

Markdown Formatting Instructions
--------------------------------

- Separate your slides with a horizontal rule (--- in markdown)
- Your slides should have a title that renders to an h1 element
- See the included slides.md for an example

Rendering Instructions
----------------------

- Put your markdown content in a file called `slides.md`
- Run `python render.py`
- Enjoy your newly generated `presentation.html`

---

Slide #2
========

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean magna tellus,
fermentum nec venenatis nec, dapibus id metus. Phasellus nulla massa, consequat
nec tempor et, elementum viverra est. Duis sed nisl in eros adipiscing tempor.

Section #1
----------

Integer in dignissim ipsum. Integer pretium nulla at elit facilisis eu feugiat
velit consectetur.

Section #2
----------

Donec risus tortor, dictum sollicitudin ornare eu, egestas at purus. Cras
consequat lacus vitae lectus faucibus et molestie nisl gravida. Donec tempor,
tortor in varius vestibulum, mi odio laoreet magna, in hendrerit nibh neque eu
eros.

---

Slide #3
========

**Hello Gentlemen**

- Mega Man 2
- Mega Man 3
- Spelunky
- Dungeon Crawl Stone Soup
- Etrian Odyssey

*Are you prepared to see beyond the veil of reason?* - DeceasedCrab

- Black Cascade
- Two Hunters
- Diadem of 12 Stars

---

Slide #4
========

render.py
---------

    import jinja2
    import markdown

    with open('presentation.html', 'w') as outfile:
        slides_src = markdown.markdown(open('slides.md').read()).split('<hr />\n')

        slides = []

        for slide_src in slides_src:
            header, content = slide_src.split('\n', 1)
            slides.append({'header': header, 'content': content})

        template = jinja2.Template(open('base.html').read())

        outfile.write(template.render({'slides': slides}))

