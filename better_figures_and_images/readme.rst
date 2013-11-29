Summary
===========

This plug-in:

- Adds a `style="width: ???px; height: auto;"` attribute to any `<img>` tags in the content, by checking
the dimensions of the image file and adding the appropriate `style="width: ???px; height: auto;"` to the `<img>` tag.
- Also finds any `div class="figures"` tags in the content, that contain images and adds the same style to them too.
- If RESPONSIVE_IMAGES setting is true, it adds `style="width: ???px; max-width: 100%; height: auto;"` instead.
- Corrects Alt text: If an img alt attribute = the image filename, it sets it to ""
- Inserts figure numbers into figure captions, if FIGURE_NUMBERS == True in global config, or figure_numbers exists in article metadata.


Assuming that the image is 250px wide, it turns output like this:

	<div class="figure">
	    <img alt="/static/images/image.jpg" src="/static/images/image.jpg" />
	    <p class="caption">
	        This is the caption of the figure.
	    </p>
	    <div class="legend">
	        Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
	        tempor incididunt ut labore et dolore magna aliqua.
	    </div>
	</div>

into output like this:

	<div class="figure" style="width: 250px; height: auto;">
	    <img style="width: 250px; height: auto;" alt="" src="/static/images/image.jpg" />
	    <p class="caption">
	        This is the caption of the figure.
	    </p>
	    <div class="legend">
	        Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
	        tempor incididunt ut labore et dolore magna aliqua.
	    </div>
	</div>

or this, if RESPONSIVE_IMAGES = True:

	<div class="figure" style="width: 250px; max-width: 100%; height: auto;">
	    <img style="width: 250px; max-width: 100%; height: auto;" alt="" src="/static/images/image.jpg" />
	    <p class="caption">
	        This is the caption of the figure.
	    </p>
	    <div class="legend">
	        Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
	        tempor incididunt ut labore et dolore magna aliqua.
	    </div>
	</div>


or this, if FIGURE_NUMBERS is also True:

    <div class="figure" style="width: 250px; max-width: 100%; height: auto;">
        <img style="width: 250px; max-width: 100%; height: auto;" alt="" src="/static/images/image.jpg" />
        <p class="caption">
            <span class="fig_num" id="fig_1">Figure 1: </span>This is the caption of the figure.
        </p>
        <div class="legend">
            Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
            tempor incididunt ut labore et dolore magna aliqua.
        </div>
    </div>

Requirements
============

This plugin requires BeautifulSoup and PIL/Pillow:

.. code-block:: bash

	pip install beautifulsoup4 Pillow

PIL/Pillow have binary modules, which pip will need to build on install - this requires some pre-requisites installed first:

.. code-block:: bash

    sudo apt-get install python-dev libxml2-dev libxslt1-dev
