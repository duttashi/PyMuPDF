Change Logs
===============

------

**Changes in Version 1.18.18**

* **Fixed** issue `#1257 <https://github.com/pymupdf/PyMuPDF/issues/1257>`_. Removing the read-only flag from PDF fields is now possible.

* **Fixed** issue `#1252 <https://github.com/pymupdf/PyMuPDF/issues/1252>`_. Now correctly specifying the ``zoom`` value for PDF link annotations.

* **Fixed** issue `#1244 <https://github.com/pymupdf/PyMuPDF/issues/1244>`_. Now correctly computing the transform matrix in :meth:`Page.get_image__bbox`.

* **Fixed** issue `#1241 <https://github.com/pymupdf/PyMuPDF/issues/1241>`_. Prevent returning artifact characters in :meth:`Page.get_textbox`, which happened in certain constellations.

* **Fixed** issue `#1234 <https://github.com/pymupdf/PyMuPDF/issues/1234>`_. Avoid creating infinite rectangles in corner cases -- :meth:`Page.get_drawings`, :meth:`Page.get_cdrawings`.

* **Added** test data and test scripts to the source PyPI source distribution.

------

**Changes in Version 1.18.17**

Focus of this version are major performance improvements of selected functions.

* **Fixed** issue `#1199 <https://github.com/pymupdf/PyMuPDF/issues/1199>`_. Using a non-existing page number in :meth:`Document.get_page_images` and friends will no longer lead to segfaults.

* **Changed** :meth:`Page.get_drawings` to now differentiate between "stroke", "fill" and combined paths. Paths containing more than one rectangle are now supported. Extracting "clipped" paths is now available as an option.

* **Added** :meth:`Page.get_cdrawings`, performance-optimized version of :meth:`Page.get_drawings`.

* **Added** :attr:`Pixmap.samples_mv`, *memoryview* of a pixmap's pixel area. Does not copy and thus always accesses the current state of that area.

* **Added** :attr:`Pixmap.samples_ptr`, Python "pointer" to a pixmap's pixel area. Allows much faster creation (factor 800+) of Qt images.



------

**Changes in Version 1.18.16**

* **Fixed** issue `#1184 <https://github.com/pymupdf/PyMuPDF/issues/1184>`_. Existing PDF widget fonts in a PDF are now accepted (i.e. not forcedly changed to a Base-14 font).

* **Fixed** issue `#1154 <https://github.com/pymupdf/PyMuPDF/issues/1154>`_. Text search hits should now be correct when ``clip`` is specified.

* **Fixed** issue `#1152 <https://github.com/pymupdf/PyMuPDF/issues/1152>`_.

* **Fixed** issue `#1146 <https://github.com/pymupdf/PyMuPDF/issues/1146>`_.

* **Added** :attr:`Link.flags` and :meth:`Link.set_flags` to the :ref:`Link` class. Implements enhancement requests `#1187 <https://github.com/pymupdf/PyMuPDF/issues/1187>`_.

* **Added** option to *simulate* :meth:`TextWriter.fill_textbox` output for predicting the number of lines, that a given text would occupy in the textbox.

* **Added** text output support as subcommand `gettext` to the ``fitz`` CLI module. Most importantly, original **physical text layout** reproduction is now supported.


------

**Changes in Version 1.18.15**

* **Fixed** issue `#1088 <https://github.com/pymupdf/PyMuPDF/issues/1088>`_. Removing an annotation's fill color should now work again both ways, using the ``fill_color=[]`` argument in :meth:`Annot.update` as well as ``fill=[]`` in :meth:`Annot.set_colors`.

* **Fixed** issue `#1081 <https://github.com/pymupdf/PyMuPDF/issues/1081>`_. :meth:`Document.subset_fonts`: fixed an error which created wrong character widths for some fonts.

* **Fixed** issue `#1078 <https://github.com/pymupdf/PyMuPDF/issues/1078>`_. :meth:`Page.get_text` and other methods related to text extraction: changed the default value of the :ref:`TextPage` ``flags`` parameter. All whitespace and :data:`ligatures` are now preserved.

* **Fixed** issue `#1085 <https://github.com/pymupdf/PyMuPDF/issues/1085>`_. The old *snake_cased* alias of ``fitz.detTextlength`` is now defined correctly.

* **Changed** :meth:`Document.subset_fonts` will now correctly prefix font subsets with an appropriate six letter uppercase tag, complying with the PDF specification.

* **Added** new method :meth:`Widget.button_states` which returns the possible values that a button-type field can have when being set to "on" or "off".

* **Added** support of text with **Small Capital** letters to the :ref:`Font` and :ref:`TextWriter` classes. This is reflected by an additional bool parameter ``small_caps`` in various of their methods.


------

**Changes in Version 1.18.14**

* **Finished** implementing new, "snake_cased" names for methods and properties, that were "camelCased" and awkward in many aspects. At the end of this documentation, there is section :ref:`Deprecated` with more background and a mapping of old to new names.

* **Fixed** issue `#1053 <https://github.com/pymupdf/PyMuPDF/issues/1053>`_. :meth:`Page.insert_image`: when given, include image mask in the hash computation.

* **Fixed** issue `#1043 <https://github.com/pymupdf/PyMuPDF/issues/1043>`_. Added ``Pixmap.getPNGdata`` to the aliases of :meth:`Pixmap.tobytes`.

* **Fixed** an internal error when computing the envelopping rectangle of drawn paths as returned by :meth:`Page.get_drawings`.

* **Fixed** an internal error occasionally causing loops when outputting text via :meth:`TextWriter.fill_textbox`.

* **Added** :meth:`Font.char_lengths`, which returns a tuple of character widths of a string.

* **Added** more ways to specify pages in :meth:`Document.delete_pages`. Now a sequence (list, tuple or range) can be specified, and the Python ``del`` statement can be used. In the latter case, Python ``slices`` are also accepted.

* **Changed** :meth:`Document.del_toc_item`, which disables a single item of the TOC: previously, the title text was removed. Instead, now the complete item will be shown grayed-out by supporting viewers.


------

**Changes in Version 1.18.13**

* **Fixed** issue `#1014 <https://github.com/pymupdf/PyMuPDF/issues/1014>`_.
* **Fixed** an internal memory leak when computing image bboxes -- :meth:`Page.get_image_bbox`.
* **Added** support for low-level access and modification of the PDF trailer. Applies to :meth:`Document.xref_get_keys`, :meth:`Document.xref_get_key`, and :meth:`Document.xref_set_key`.
* **Added** documentation for maintaining private entries in PDF metadata.
* **Added** documentation for handling transparent image insertions, :meth:`Page.insert_image`.
* **Added** :meth:`Page.get_image_rects`, an improved version of :meth:`Page.get_image_bbox`.
* **Changed** :meth:`Document.delete_pages` to support various ways of specifying pages to delete. Implements `#1042 <https://github.com/pymupdf/PyMuPDF/issues/1042>`_.
* **Changed** :meth:`Page.insert_image` to also accept the xref of an existing image in the file. This allows "copying" images between pages, and extremely fast mutiple insertions.
* **Changed** :meth:`Page.insert_image` to also accept the integer parameter ``alpha``. To be used for performance improvements.
* **Changed** :meth:`Pixmap.set_alpha` to support new parameters for pre-multiplying colors with their alpha values and setting a specific color to fully transparent (e.g. white).
* **Changed** :meth:`Document.embfile_add` to automatically set creation and modification date-time. Correspondingly, :meth:`Document.embfile_upd` automatically maintains modification date-time (``/ModDate`` PDF key), and :meth:`Document.embfile_info` correspondingly reports these data. In addition, the embedded file's associated "collection item" is included via its :data:`xref`. This supports the development of PDF portfolio applications.

------

**Changes in Version 1.18.11 / 1.18.12**

* **Fixed** issue `#972 <https://github.com/pymupdf/PyMuPDF/issues/972>`_. Improved layout of source distribution material.
* **Fixed** issue `#962 <https://github.com/pymupdf/PyMuPDF/issues/962>`_. Stabilized Linux distribution detection for generating PyMuPDF from sources.
* **Added:** :meth:`Page.get_xobjects` delivers the result of :meth:`Document.get_page_xobjects`.
* **Added:** :meth:`Page.get_image_info` delivers meta information for all images shown on the page.
* **Added:** :meth:`Tools.mupdf_display_warnings` allows setting on / off the display of MuPDF-generated warnings. The default is off.
* **Added:** :meth:`Document.ez_save` convenience alias of :meth:`Document.save` with some different defaults.
* **Changed:** Image extractions of document pages now also contain the image's **transformation matrix**. This concerns :meth:`Page.get_image_bbox` and the DICT, JSON, RAWDICT, and RAWJSON variants of :meth:`Page.get_text`.


------

**Changes in Version 1.18.10**

* **Fixed** issue `#941 <https://github.com/pymupdf/PyMuPDF/issues/941>`_. Added old aliases for :meth:`DisplayList.get_pixmap` and :meth:`DisplayList.get_textpage`.
* **Fixed** issue `#929 <https://github.com/pymupdf/PyMuPDF/issues/929>`_. Stabilized removal of JavaScript objects with :meth:`Document.scrub`.
* **Fixed** issue `#927 <https://github.com/pymupdf/PyMuPDF/issues/927>`_. Removed a loop in the reworked :meth:`TextWriter.fill_textbox`.
* **Changed** :meth:`Document.xref_get_keys` and :meth:`Document.xref_get_key` to also allow accessing the PDF trailer dictionary. This can be done by using `-1` as the xref number argument.
* **Added** a number of functions for reconstructing the quads for text lines, spans and characters extracted by :meth:`Page.get_text` options "dict" and "rawdict". See :meth:`recover_quad` and friends.
* **Added** :meth:`Tools.unset_quad_corrections` to suppress character quad corrections (occasionally required for erroneous fonts).

------

**Changes in Version 1.18.9**


* **Fixed** issue `#888 <https://github.com/pymupdf/PyMuPDF/issues/888>`_. Removed ambiguous statements concerning PyMuPDF's license, which is now clearly stated to be GNU AGPL V3.
* **Fixed** issue `#895 <https://github.com/pymupdf/PyMuPDF/issues/895>`_.
* **Fixed** issue `#896 <https://github.com/pymupdf/PyMuPDF/issues/896>`_. Since v1.17.6 PyMuPDF suppresses the font subset tags and only reports the base fontname in text extraction outputs "dict" / "json" / "rawdict" / "rawjson". Now a new global parameter can request the old behaviour, :meth:`Tools.set_subset_fontnames`.
* **Fixed** issue `#885 <https://github.com/pymupdf/PyMuPDF/issues/885>`_. Pixmap creation now also works with filenames given as ``pathlib.Paths``.
* **Changed** :meth:`Document.subset_fonts`: Text is **not rewritten** any more and should therefore **retain all its origial properties** -- like being hidden or being controlled by Optional Content mechanisms.
* **Changed** :ref:`TextWriter` output to also accept text in right to left mode (Arabian, Hebrew): :meth:`TextWriter.fill_textbox`, :meth:`TextWriter.append`. These methods now accept a new boolean parameter `right_to_left`, which is *False* by default. Implements `#897 <https://github.com/pymupdf/PyMuPDF/issues/897>`_.
* **Changed** :meth:`TextWriter.fill_textbox` to return all lines of text, that did not fit in the given rectangle. Also changed the default of the ``warn`` parameter to no longer print a warning message in overflow situations.
* **Added** a utility function :meth:`recover_quad`, which computes the quadrilateral of a span. This function can be used for correctly marking text extracted with the "dict" or "rawdict" options of :meth:`Page.get_text`.

------

**Changes in Version 1.18.8**


This is a bug fix version only. We are publishing early because of the potentially widely used functions.

* **Fixed** issue `#881 <https://github.com/pymupdf/PyMuPDF/issues/881>`_. Fixed a memory leak in :meth:`Page.insert_image` when inserting images from files or memory.
* **Fixed** issue `#878 <https://github.com/pymupdf/PyMuPDF/issues/878>`_. ``pathlib.Path`` objects should now correctly handle file path hierarchies.


------

**Changes in Version 1.18.7**


* **Added** an experimental :meth:`Document.subset_fonts` which reduces the size of eligible fonts based on their use by text in the PDF. Implements `#855 <https://github.com/pymupdf/PyMuPDF/discussions/855>`_.
* **Implemented** request `#870 <https://github.com/pymupdf/PyMuPDF/pull/870>`_: :meth:`Document.convert_to_pdf` now also supports PDF documents.
* **Renamed** ``Document.write`` to :meth:`Document.tobytes` for greater clarity. But the deprecated name remains available for some time.
* **Implemented** request `#843 <https://github.com/pymupdf/PyMuPDF/Discussions/843>`_: :meth:`Document.tobytes` now supports linearized PDF output. :meth:`Document.save` now also supports writing to Python **file objects**. In addition, the open function now also supports Python file objects.
* **Fixed** issue `#844 <https://github.com/pymupdf/PyMuPDF/issues/844>`_.
* **Fixed** issue `#838 <https://github.com/pymupdf/PyMuPDF/issues/838>`_.
* **Fixed** issue `#823 <https://github.com/pymupdf/PyMuPDF/issues/823>`_. More logic for better support of OCR-ed text output (Tesseract, ABBYY).
* **Fixed** issue `#818 <https://github.com/pymupdf/PyMuPDF/issues/818>`_.
* **Fixed** issue `#814 <https://github.com/pymupdf/PyMuPDF/issues/814>`_.
* **Added** :meth:`Document.get_page_labels` which returns a list of page label definitions of a PDF.
* **Added** :meth:`Document.has_annots` and :meth:`Document.has_links` to check whether these object types are present anywhere in a PDF.
* **Added** expert low-level functions to simplify inquiry and modification of PDF object sources: :meth:`Document.xref_get_keys` lists the keys of object :data:`xref`, :meth:`Document.xref_get_key` returns type and content of a key, and :meth:`Document.xref_set_key` modifies the key's value.
* **Added** parameter ``thumbnails`` to :meth:`Document.scrub` to also allow removing page thumbnail images.
* **Improved** documentation for how to add valid text marker annotations for non-horizontal text.

We continued the process of renaming methods and properties from *"mixedCase"* to *"snake_case"*. Documentation usually mentions the new names only, but old, deprecated names remain available for some time.



------

**Changes in Version 1.18.6**

* **Fixed** issue `#812 <https://github.com/pymupdf/PyMuPDF/issues/812>`_.
* **Fixed** issue `#793 <https://github.com/pymupdf/PyMuPDF/issues/793>`_. Invalid document metadata previously prevented opening some documents at all. This error has been removed.
* **Fixed** issue `#792 <https://github.com/pymupdf/PyMuPDF/issues/792>`_. Text search and text extraction will make no rectangle containment checks at all if the default ``clip=None`` is used.
* **Fixed** issue `#785 <https://github.com/pymupdf/PyMuPDF/issues/785>`_.
* **Fixed** issue `#780 <https://github.com/pymupdf/PyMuPDF/issues/780>`_. Corrected a parameter check error.
* **Fixed** issue `#779 <https://github.com/pymupdf/PyMuPDF/issues/779>`_. Fixed typo
* **Added** an option to set the desired line height for text boxes. Implements `#804 <https://github.com/pymupdf/PyMuPDF/issues/804>`_.
* **Changed** text position retrieval to better cope with Tesseract's glyphless font. Implements `#803 <https://github.com/pymupdf/PyMuPDF/issues/803>`_.
* **Added** an option to choose the prefix of new annotations, fields and links for providing unique annotation ids. Implements request `#807 <https://github.com/pymupdf/PyMuPDF/issues/807>`_.
* **Added** getting and setting color and text properties for Table of Contents items for PDFs. Implements `#779 <https://github.com/pymupdf/PyMuPDF/issues/779>`_.
* **Added** PDF page label handling: :meth:`Page.get_label()` returns the page label, :meth:`Document.get_page_numbers` return all page numbers having a specified label, and :meth:`Document.set_page_labels` adds or updates a PDF's page label definition.



.. note::
   This version introduces **Python type hinting**. The goal is to provide each parameter and the return value of all functions and methods with type information. This still is work in progress although the majority of functions has already been handled.


------

**Changes in Version 1.18.5**

Apart from several fixes, this version also focusses on several minor, but important feature improvements. Among the latter is a more precise computation of proper line heights and insertion points for writing / inserting text. As opposed to using font-agnostic constants, these values are now taken from the font's properties.

Also note that this is the first version which does no longer provide pregenerated wheels for Python versions older than 3.6. PIP also discontinues support for these by end of this year 2020.

* **Fixed** issue `#771 <https://github.com/pymupdf/PyMuPDF/issues/771>`_. By using "small glyph heights" option, the full page text can be extracted.
* **Fixed** issue `#768 <https://github.com/pymupdf/PyMuPDF/issues/768>`_.
* **Fixed** issue `#750 <https://github.com/pymupdf/PyMuPDF/issues/750>`_.
* **Fixed** issue `#739 <https://github.com/pymupdf/PyMuPDF/issues/739>`_. The "dict", "rawdict" and corresponding JSON output variants now have two new *span* keys: ``"ascender"`` and ``"descender"``. These floats represent special font properties which can be used to compute bboxes of spans or characters of **exactly fontsize height** (as opposed to the default line height). An example algorithm is shown in section "Span Dictionary" `here <https://pymupdf.readthedocs.io/en/latest/textpage.html#dictionary-structure-of-extractdict-and-extractrawdict>`_. Also improved the detection and correction of ill-specified ascender / descender values encountered in some fonts.
* **Added** a new, experimental :meth:`Tools.set_small_glyph_heights` -- also in response to issue `#739 <https://github.com/pymupdf/PyMuPDF/issues/739>`_. This method sets or unsets a global parameter to **always compute bboxes with fontsize height**. If "on", text searching and all text extractions will returned rectangles, bboxes and quads with a smaller height.
* **Fixed** issue `#728 <https://github.com/pymupdf/PyMuPDF/issues/728>`_.
* **Changed** fill color logic of 'Polyline' annotations: this parameter now only pertains to line end symbols -- the annotation itself can no longer have a fill color. Also addresses issue `#727 <https://github.com/pymupdf/PyMuPDF/issues/727>`_.
* **Changed** :meth:`Page.getImageBbox` to also compute the bbox if the image is contained in an XObject.
* **Changed** :meth:`Shape.insertTextbox`, resp. :meth:`Page.insertTextbox`, resp. :meth:`TextWriter.fillTextbox` to respect font's properties "ascender" / "descender" when computing line height and insertion point. This should no longer lead to line overlaps for multi-line output. These methods used to ignore font specifics and used constant values instead.


------

**Changes in Version 1.18.4**

This version adds several features to support PDF Optional Content. Among other things, this includes OCMDs (Optional Content Membership Dictionaries) with the full scope of *"visibility expressions"* (PDF key ``/VE``), text insertions (including the :ref:`TextWriter` class) and drawings.

* **Fixed** issue `#727 <https://github.com/pymupdf/PyMuPDF/issues/727>`_. Freetext annotations now support an uncolored rectangle when ``fill_color=None``.
* **Fixed** issue `#726 <https://github.com/pymupdf/PyMuPDF/issues/726>`_. UTF-8 encoding errors are now handled for HTML / XML :meth:`Page.getText` output.
* **Fixed** issue `#724 <https://github.com/pymupdf/PyMuPDF/issues/724>`_. Empty values are no longer stored in the PDF /Info metadata dictionary.
* **Added** new methods :meth:`Document.set_oc` and :meth:`Document.get_oc` to set or get optional content references for **existing** image and form XObjects. These methods are similar to the same-named methods of :ref:`Annot`.
* **Added** :meth:`Document.set_ocmd`, :meth:`Document.get_ocmd` for handling OCMDs.
* **Added** **Optional Content** support for text insertion and drawing.
* **Added** new method :meth:`Page.deleteWidget`, which deletes a form field from a page. This is analogous to deleting annotations.
* **Added** support for Popup annotations. This includes defining the Popup rectangle and setting the Popup to open or closed. Methods / attributes :meth:`Annot.set_popup`, :meth:`Annot.set_open`, :attr:`Annot.has_popup`, :attr:`Annot.is_open`, :attr:`Annot.popup_rect`, :attr:`Annot.popup_xref`.

Other changes:

* The **naming of methods and attributes** in PyMuPDF is far from being satisfactory: we have *CamelCases*, *mixedCases* and *lower_case_with_underscores* all over the place. With the :ref:`Annot` as the first candidate, we have started an activity to clean this up step by step, converting to lower case with underscores for methods and attributes while keeping UPPERCASE for the constants.

   - Old names will remain available to prevent code breaks, but they will no longer be mentioned in the documentation.
   - New methods and attributes of all classes will be named according to the new standard.

------

**Changes in Version 1.18.3**

As a major new feature, this version introduces support for PDF's **Optional Content** concept.

* **Fixed** issue `#714 <https://github.com/pymupdf/PyMuPDF/issues/714>`_.
* **Fixed** issue `#711 <https://github.com/pymupdf/PyMuPDF/issues/711>`_.
* **Fixed** issue `#707 <https://github.com/pymupdf/PyMuPDF/issues/707>`_: if a PDF user password, but no owner password is supplied nor present, then the user password is also used as the owner password.
* **Fixed** ``expand`` and ``deflate`` parameters of methods :meth:`Document.save` and :meth:`Document.write`. Individual image and font compression should now finally work. Addresses issue `#713 <https://github.com/pymupdf/PyMuPDF/issues/713>`_.
* **Added** a support of PDF optional content. This includes several new :ref:`Document` methods for inquiring and setting optional content status and adding optional content configurations and groups. In addition, images, form XObjects and annotations now can be bound to optional content specifications. **Resolved** issue `#709 <https://github.com/pymupdf/PyMuPDF/issues/709>`_.



------

**Changes in Version 1.18.2**

This version contains some interesting improvements for text searching: any number of search hits is now returned and the **hit_max** parameter was removed. The new **clip** parameter in addition allows to restrict the search area. Searching now detects hyphenations at line breaks and accordingly finds hyphenated words.

* **Fixed** issue `#575 <https://github.com/pymupdf/PyMuPDF/issues/575>`_: if using ``quads=False`` in text searching, then overlapping rectangles on the same line are joined. Previously, parts of the search string, which belonged to different "marked content" items, each generated their own rectangle -- just as if occurring on separate lines.
* **Added** :attr:`Document.isRepaired`, which is true if the PDF was repaired on open.
* **Added** :meth:`Document.setXmlMetadata` which either updates or creates PDF XML metadata. Implements issue `#691 <https://github.com/pymupdf/PyMuPDF/issues/691>`_.
* **Added** :meth:`Document.getXmlMetadata` returns PDF XML metadata.
* **Changed** creation of PDF documents: they will now always carry a PDF identification (``/ID`` field) in the document trailer. Implements issue `#691 <https://github.com/pymupdf/PyMuPDF/issues/691>`_.
* **Changed** :meth:`Page.searchFor`: a new parameter ``clip`` is accepted to restrict the search to this rectangle. Correspondingly, the attribute :attr:`TextPage.rect` is now respected by :meth:`TextPage.search`.
* **Changed** parameter ``hit_max`` in :meth:`Page.searchFor` and :meth:`TextPage.search` is now obsolete: methods will return all hits.
* **Changed** character **selection criteria** in :meth:`Page.getText`: a character is now considered to be part of a ``clip`` if its bbox is fully contained. Before this, a non-empty intersection was sufficient.
* **Changed** :meth:`Document.scrub` to support a new option `redact_images`. This addresses issue `#697 <https://github.com/pymupdf/PyMuPDF/issues/697>`_.


------

**Changes in Version 1.18.1**

* **Fixed** issue `#692 <https://github.com/pymupdf/PyMuPDF/issues/692>`_. PyMuPDF now detects and recovers from more cyclic resource dependencies in PDF pages and for the first time reports them in the MuPDF warnings store.
* **Fixed** issue `#686 <https://github.com/pymupdf/PyMuPDF/issues/686>`_.
* **Added** opacity options for the :ref:`Shape` class: Stroke and fill colors can now be set to some transparency value. This means that all :ref:`Page` draw methods, methods :meth:`Page.insertText`, :meth:`Page.insertTextbox`, :meth:`Shape.finish`, :meth:`Shape.insertText`, and :meth:`Shape.insertTextbox` support two new parameters: *stroke_opacity* and *fill_opacity*.
* **Added** new parameter ``mask`` to :meth:`Page.insertImage` for optionally providing an external image mask. Resolves issue `#685 <https://github.com/pymupdf/PyMuPDF/issues/685>`_.
* **Added** :meth:`Annot.soundGet` for extracting the sound of an audio annotation.

------

**Changes in Version 1.18.0**

This is the first PyMuPDF version supporting MuPDF v1.18. The focus here is on extending PyMuPDF's own functionality -- apart from bug fixing. Subsequent PyMuPDF patches may address features new in MuPDF.

* **Fixed** issue `#519 <https://github.com/pymupdf/PyMuPDF/issues/519>`_. This upstream bug occurred occasionally for some pages only and seems to be fixed now: page layout should no longer be ruined in these cases.

* **Fixed** issue `#675 <https://github.com/pymupdf/PyMuPDF/issues/675>`_.

  - Unsuccessful storage allocations should now always lead to exceptions (circumvention of an upstream bug intermittently crashing the interpreter).
  - :ref:`Pixmap` size is now based on ``size_t`` instead of ``int`` in C and should be correct even for extremely large pixmaps.

* **Fixed** issue `#668 <https://github.com/pymupdf/PyMuPDF/issues/668>`_. Specification of dashes for PDF drawing insertion should now correctly reflect the PDF spec.
* **Fixed** issue `#669 <https://github.com/pymupdf/PyMuPDF/issues/669>`_. A major source of memory leakage in :meth:`Page.insert_pdf` has been removed.
* **Added** keyword *"images"* to :meth:`Page.apply_redactions` for fine-controlling the handling of images.
* **Added** :meth:`Annot.getText` and :meth:`Annot.getTextbox`, which offer the same functionality as the :ref:`Page` versions.
* **Added** key *"number"* to the block dictionaries of :meth:`Page.getText` / :meth:`Annot.getText` for options "dict" and "rawdict".
* **Added** :meth:`glyph_name_to_unicode` and :meth:`unicode_to_glyph_name`. Both functions do not really connect to a specific font and are now independently available, too. The data are now based on the `Adobe Glyph List <https://github.com/adobe-type-tools/agl-aglfn/blob/master/glyphlist.txt>`_.
* **Added** convenience functions :meth:`adobe_glyph_names` and :meth:`adobe_glyph_unicodes` which return the respective available data.
* **Added** :meth:`Page.getDrawings` which returns details of drawing operations on a document page. Works for all document types.
* Improved performance of :meth:`Document.insert_pdf`. Multiple object copies are now also suppressed across multiple separate insertions from the same source. This saves time, memory and target file size. Previously this mechanism was only active within each single method execution. The feature can also be suppressed with the new method bool parameter *final=1*, which is the default.
* For PNG images created from pixmaps, the resolution (dpi) is now automatically set from the respective :attr:`Pixmap.xres` and :attr:`Pixmap.yres` values.


------

**Changes in Version 1.17.7**

* **Fixed** issue `#651 <https://github.com/pymupdf/PyMuPDF/issues/651>`_. An upstream bug causing interpreter crashes in corner case redaction processings was fixed by backporting MuPDF changes from their development repo.
* **Fixed** issue `#645 <https://github.com/pymupdf/PyMuPDF/issues/645>`_. Pixmap top-left coordinates can be set (again) by their own method, :meth:`Pixmap.set_origin`.
* **Fixed** issue `#622 <https://github.com/pymupdf/PyMuPDF/issues/622>`_. :meth:`Page.insertImage` again accepts a :data:`rect_like` parameter.
* **Added** severeal new methods to improve and speed-up table of contents (TOC) handling. Among other things, TOC items can now changed or deleted individually -- without always replacing the complete TOC. Furthermore, access to some PDF page attributes is now possible without first **loading** the page. This has a very significant impact on the performance of TOC manipulation.
* **Added** an option to :meth:`Document.insert_pdf` which allows displaying progress messages. Adresses `#640 <https://github.com/pymupdf/PyMuPDF/issues/640>`_.
* **Added** :meth:`Page.getTextbox` which extracts text contained in a rectangle. In many cases, this should obsolete writing your own script for this type of thing.
* **Added** new ``clip`` parameter to :meth:`Page.getText` to simplify and speed up text extraction of page sub areas.
* **Added** :meth:`TextWriter.appendv` to add text in **vertical write mode**. Addresses issue `#653 <https://github.com/pymupdf/PyMuPDF/issues/653>`_


------

**Changes in Version 1.17.6**

* **Fixed** issue `#605 <https://github.com/pymupdf/PyMuPDF/issues/605>`_
* **Fixed** issue `#600 <https://github.com/pymupdf/PyMuPDF/issues/600>`_ -- text should now be correctly positioned also for pages with a CropBox smaller than MediaBox.
* **Added** text span dictionary key ``origin`` which contains the lower left coordinate of the first character in that span.
* **Added** attribute :attr:`Font.buffer`, a *bytes* copy of the font file.
* **Added** parameter *sanitize* to :meth:`Page.cleanContents`. Allows switching of sanitization, so only syntax cleaning will be done.

------

**Changes in Version 1.17.5**

* **Fixed** issue `#561 <https://github.com/pymupdf/PyMuPDF/issues/561>`_ -- second go: certain :ref:`TextWriter` usages with many alternating fonts did not work correctly.
* **Fixed** issue `#566 <https://github.com/pymupdf/PyMuPDF/issues/566>`_.
* **Fixed** issue `#568 <https://github.com/pymupdf/PyMuPDF/issues/568>`_.
* **Fixed** -- opacity is now correctly taken from the :ref:`TextWriter` object, if not given in :meth:`TextWriter.writeText`.
* **Added** a new global attribute :attr:`fitz_fontdescriptors`. Contains information about usable fonts from repository `pymupdf-fonts <https://github.com/pymupdf/pymupdf-fonts>`_.
* **Added** :meth:`Font.valid_codepoints` which returns an array of unicode codepoints for which the font has a glyph.
* **Added** option ``text_as_path`` to :meth:`Page.getSVGimage`. this implements `#580 <https://github.com/pymupdf/PyMuPDF/issues/580>`_. Generates much smaller SVG files with parseable text if set to *False*.


------

**Changes in Version 1.17.4**

* **Fixed** issue `#561 <https://github.com/pymupdf/PyMuPDF/issues/561>`_. Handling of more than 10 :ref:`Font` objects on one page should now work correctly.
* **Fixed** issue `#562 <https://github.com/pymupdf/PyMuPDF/issues/562>`_. Annotation pixmaps are no longer derived from the page pixmap, thus avoiding unintended inclusion of page content.
* **Fixed** issue `#559 <https://github.com/pymupdf/PyMuPDF/issues/559>`_. This **MuPDF** bug is being temporarily fixed with a pre-version of MuPDF's next release.
* **Added** utility function :meth:`repair_mono_font` for correcting displayed character spacing for some mono-spaced fonts.
* **Added** utility method :meth:`Document.need_appearances` for fine-controlling Form PDF behavior. Addresses issue `#563 <https://github.com/pymupdf/PyMuPDF/issues/563>`_.
* **Added** utility function :meth:`sRGB_to_pdf` to recover the PDF color triple for a given color integer in sRGB format.
* **Added** utility function :meth:`sRGB_to_rgb` to recover the (R, G, B) color triple for a given color integer in sRGB format.
* **Added** utility function :meth:`make_table` which delivers table cells for a given rectangle and desired numbers of columns and rows.
* **Added** support for optional fonts in repository `pymupdf-fonts <https://github.com/pymupdf/pymupdf-fonts>`_.

------

**Changes in Version 1.17.3**

* **Fixed** an undocumented issue, which prevented fully cleaning a PDF page when using :meth:`Page.cleanContents`.
* **Fixed** issue `#540 <https://github.com/pymupdf/PyMuPDF/issues/540>`_. Text extraction for EPUB should again work correctly.
* **Fixed** issue `#548 <https://github.com/pymupdf/PyMuPDF/issues/548>`_. Documentation now includes ``LINK_NAMED``.
* **Added** new parameter to control start of text in :meth:`TextWriter.fillTextbox`. Implements `#549 <https://github.com/pymupdf/PyMuPDF/issues/549>`_.
* **Changed** documentation of :meth:`Page.add_redact_annot` to explain the usage of non-builtin fonts.

------

**Changes in Version 1.17.2**

* **Fixed** issue `#533 <https://github.com/pymupdf/PyMuPDF/issues/533>`_.
* **Added** options to modify 'Redact' annotation appearance. Implements `#535 <https://github.com/pymupdf/PyMuPDF/issues/535>`_.


------

**Changes in Version 1.17.1**

* **Fixed** issue `#520 <https://github.com/pymupdf/PyMuPDF/issues/520>`_.
* **Fixed** issue `#525 <https://github.com/pymupdf/PyMuPDF/issues/525>`_. Vertices for 'Ink' annots should now be correct.
* **Fixed** issue `#524 <https://github.com/pymupdf/PyMuPDF/issues/524>`_. It is now possible to query and set rotation for applicable annotation types.

Also significantly improved inline documentation for better support of interactive help.

------

**Changes in Version 1.17.0**

This version is based on MuPDF v1.17. Following are highlights of new and changed features:

* **Added** extended language support for annotations and widgets: a mixture of Latin, Greece, Russian, Chinese, Japanese and Korean characters can now be used in 'FreeText' annotations and text widgets. No special arrangement is required to use it.

* Faster page access is implemented for documents supporting a "chapter" structure. This applies to EPUB documents currently. This comes with several new :ref:`Document` methods and changes for :meth:`Document.loadPage` and the "indexed" page access *doc[n]*: In addition to specifying a page number as before, a tuple *(chaper, pno)* can be specified to identify the desired page.

* **Changed:** Improved support of redaction annotations: images overlapped by redactions are **permanantly modified** by erasing the overlap areas. Also links are removed if overlapped by redactions. This is now fully in sync with PDF specifications.

Other changes:

* **Changed** :meth:`TextWriter.writeText` to support the *"morph"* parameter.
* **Added** methods :meth:`Rect.morph`, :meth:`IRect.morph`, and :meth:`Quad.morph`, which return a new :ref:`Quad`.
* **Changed** :meth:`Page.add_freetext_annot` to support text alignment via a new *"align"* parameter.
* **Fixed** issue `#508 <https://github.com/pymupdf/PyMuPDF/issues/508>`_. Improved image rectangle calculation to hopefully deliver correct values in most if not all cases.
* **Fixed** issue `#502 <https://github.com/pymupdf/PyMuPDF/issues/502>`_.
* **Fixed** issue `#500 <https://github.com/pymupdf/PyMuPDF/issues/500>`_. :meth:`Document.convertToPDF` should no longer cause memory leaks.
* **Fixed** issue `#496 <https://github.com/pymupdf/PyMuPDF/issues/496>`_. Annotations and widgets / fields are now added or modified using the coordinates of the **unrotated page**. This behavior is now in sync with other methods modifying PDF pages.
* **Added** :attr:`Page.rotationMatrix` and :attr:`Page.derotationMatrix` to support coordinate transformations between the rotated and the original versions of a PDF page.

Potential code breaking changes:

* The private method ``Page._getTransformation()`` has been removed. Use the public :attr:`Page.transformationMattrix` instead.


------

**Changes in Version 1.16.18**

This version introduces several new features around PDF text output. The motivation is to simplify this task, while at the same time offering extending features.

One major achievement is using MuPDF's capabilities to dynamically choosing fallback fonts whenever a character cannot be found in the current one. This seemlessly works for Base-14 fonts in combination with CJK fonts (China, Japan, Korea). So a text may contain **any combination of characters** from the Latin, Greek, Russian, Chinese, Japanese and Korean languages.

* **Fixed** issue `#493 <https://github.com/pymupdf/PyMuPDF/issues/493>`_. ``Pixmap(doc, xref)`` should now again correctly resemble the loaded image object.
* **Fixed** issue `#488 <https://github.com/pymupdf/PyMuPDF/issues/488>`_. Widget names are now modifyable.
* **Added** new class :ref:`Font` which represents a font.
* **Added** new class :ref:`TextWriter` which serves as a container for text to be written on a page.
* **Added** :meth:`Page.writeText` to write one or more :ref:`TextWriter` objects to the page.


------

**Changes in Version 1.16.17**


* **Fixed** issue `#479 <https://github.com/pymupdf/PyMuPDF/issues/479>`_. PyMuPDF should now more correctly report image resolutions. This applies to both, images (either from images files or extracted from PDF documents) and pixmaps created from images.
* **Added** :meth:`Pixmap.set_dpi` which sets the image resolution in x and y directions.

------

**Changes in Version 1.16.16**


* **Fixed** issue `#477 <https://github.com/pymupdf/PyMuPDF/issues/477>`_.
* **Fixed** issue `#476 <https://github.com/pymupdf/PyMuPDF/issues/476>`_.
* **Changed** annotation line end symbol coloring and fixed an error coloring the interior of 'Polyline' /'Polygon' annotations.

------

**Changes in Version 1.16.14**


* **Changed** text marker annotations to accept parameters beyond just quadrilaterals such that now **text lines between two given points can be marked**.

* **Added** :meth:`Document.scrub` which **removes potentially sensitive data** from a PDF. Implements `#453 <https://github.com/pymupdf/PyMuPDF/issues/453>`_.

* **Added** :meth:`Annot.blendMode` which returns the **blend mode** of annotations.

* **Added** :meth:`Annot.setBlendMode` to set the annotation's blend mode. This resolves issue `#416 <https://github.com/pymupdf/PyMuPDF/issues/416>`_.
* **Changed** :meth:`Annot.update` to accept additional parameters for setting blend mode and opacity.
* **Added** advanced graphics features to **control the anti-aliasing values**, :meth:`Tools.set_aa_level`. Resolves `#467 <https://github.com/pymupdf/PyMuPDF/issues/467>`_

* **Fixed** issue `#474 <https://github.com/pymupdf/PyMuPDF/issues/474>`_.
* **Fixed** issue `#466 <https://github.com/pymupdf/PyMuPDF/issues/466>`_.



------

**Changes in Version 1.16.13**


* **Added** :meth:`Document.getPageXObjectList` which returns a list of **Form XObjects** of the page.
* **Added** :meth:`Page.setMediaBox` for changing the physical PDF page size.
* **Added** :ref:`Page` methods which have been internal before: :meth:`Page.cleanContents` (= :meth:`Page._cleanContents`), :meth:`Page.getContents` (= :meth:`Page._getContents`), :meth:`Page.getTransformation` (= :meth:`Page._getTransformation`).



------

**Changes in Version 1.16.12**

* **Fixed** issue `#447 <https://github.com/pymupdf/PyMuPDF/issues/447>`_
* **Fixed** issue `#461 <https://github.com/pymupdf/PyMuPDF/issues/461>`_.
* **Fixed** issue `#397 <https://github.com/pymupdf/PyMuPDF/issues/397>`_.
* **Fixed** issue `#463 <https://github.com/pymupdf/PyMuPDF/issues/463>`_.
* **Added** JavaScript support to PDF form fields, thereby fixing `#454 <https://github.com/pymupdf/PyMuPDF/issues/454>`_.
* **Added** a new annotation method :meth:`Annot.delete_responses`, which removes 'Popup' and response annotations referring to the current one. Mainly serves data protection purposes.
* **Added** a new form field method :meth:`Widget.reset`, which resets the field value to its default.
* **Changed** and extended handling of redactions: images and XObjects are removed if *contained* in a redaction rectangle. Any partial only overlaps will just be covered by the redaction background color. Now an *overlay* text can be specified to be inserted in the rectangle area to **take the place the deleted original** text. This resolves `#434 <https://github.com/pymupdf/PyMuPDF/issues/434>`_.

------

**Changes in Version 1.16.11**

* **Added** Support for redaction annotations via method :meth:`Page.add_redact_annot` and :meth:`Page.apply_redactions`.
* **Fixed** issue #426 ("PolygonAnnotation in 1.16.10 version").
* **Fixed** documentation only issues `#443 <https://github.com/pymupdf/PyMuPDF/issues/443>`_ and `#444 <https://github.com/pymupdf/PyMuPDF/issues/444>`_.

------

**Changes in Version 1.16.10**

* **Fixed** issue #421 ("annot.set_rect(rect) has no effect on text Annotation")
* **Fixed** issue #417 ("Strange behavior for page.deleteAnnot on 1.16.9 compare to 1.13.20")
* **Fixed** issue #415 ("Annot.setOpacity throws mupdf warnings")
* **Changed** all "add annotation / widget" methods to store a unique name in the */NM* PDF key.
* **Changed** :meth:`Annot.setInfo` to also accept direct parameters in addition to a dictionary.
* **Changed** :attr:`Annot.info` to now also show the annotation's unique id (*/NM* PDF key) if present.
* **Added** :meth:`Page.annot_names` which returns a list of all annotation names (*/NM* keys).
* **Added** :meth:`Page.load_annot` which loads an annotation given its unique id (*/NM* key).
* **Added** :meth:`Document.reload_page` which provides a new copy of a page after finishing any pending updates to it.


------

**Changes in Version 1.16.9**

* **Fixed** #412 ("Feature Request: Allow controlling whether TOC entries should be collapsed")
* **Fixed** #411 ("Seg Fault with page.firstWidget")
* **Fixed** #407 ("Annot.setOpacity trouble")
* **Changed** methods :meth:`Annot.setBorder`, :meth:`Annot.setColors`, :meth:`Link.setBorder`, and :meth:`Link.setColors` to also accept direct parameters, and not just cumbersome dictionaries.

------

**Changes in Version 1.16.8**

* **Added** several new methods to the :ref:`Document` class, which make dealing with PDF low-level structures easier. I also decided to provide them as "normal" methods (as opposed to private ones starting with an underscore "_"). These are :meth:`Document.xrefObject`, :meth:`Document.xrefStream`, :meth:`Document.xrefStreamRaw`, :meth:`Document.PDFTrailer`, :meth:`Document.PDFCatalog`, :meth:`Document.metadataXML`, :meth:`Document.updateObject`, :meth:`Document.updateStream`.
* **Added** :meth:`Tools.mupdf_disply_errors` which sets the display of mupdf errors on *sys.stderr*.
* **Added** a commandline facility. This a major new feature: you can now invoke several utility functions via *"python -m fitz ..."*. It should obsolete the need for many of the most trivial scripts. Please refer to :ref:`Module`.


------

**Changes in Version 1.16.7**

Minor changes to better synchronize the binary image streams of :ref:`TextPage` image blocks and :meth:`Document.extractImage` images.

* **Fixed** issue #394 ("PyMuPDF Segfaults when using TOOLS.mupdf_warnings()").
* **Changed** redirection of MuPDF error messages: apart from writing them to Python *sys.stderr*, they are now also stored with the MuPDF warnings.
* **Changed** :meth:`Tools.mupdf_warnings` to automatically empty the store (if not deactivated via a parameter).
* **Changed** :meth:`Page.getImageBbox` to return an **infinite rectangle** if the image could not be located on the page -- instead of raising an exception.


------

**Changes in Version 1.16.6**

* **Fixed** issue #390 ("Incomplete deletion of annotations").
* **Changed** :meth:`Page.searchFor` / :meth:`Document.searchPageFor` to also support the *flags* parameter, which controls the data included in a :ref:`TextPage`.
* **Changed** :meth:`Document.getPageImageList`, :meth:`Document.getPageFontList` and their :ref:`Page` counterparts to support a new parameter *full*. If true, the returned items will contain the :data:`xref` of the *Form XObject* where the font or image is referenced.

------

**Changes in Version 1.16.5**

More performance improvements for text extraction.

* **Fixed** second part of issue #381 (see item in v1.16.4).
* **Added** :meth:`Page.getTextPage`, so it is no longer required to create an intermediate display list for text extractions. Page level wrappers for text extraction and text searching are now based on this, which should improve performance by ca. 5%.

------

**Changes in Version 1.16.4**


* **Fixed** issue #381 ("TextPage.extractDICT ... failed ... after upgrading ... to 1.16.3")
* **Added** method :meth:`Document.pages` which delivers a generator iterator over a page range.
* **Added** method :meth:`Page.links` which delivers a generator iterator over the links of a page.
* **Added** method :meth:`Page.annots` which delivers a generator iterator over the annotations of a page.
* **Added** method :meth:`Page.widgets` which delivers a generator iterator over the form fields of a page.
* **Changed** :attr:`Document.is_form_pdf` to now contain the number of widgets, and *False* if not a PDF or this number is zero.


------

**Changes in Version 1.16.3**

Minor changes compared to version 1.16.2. The code of the "dict" and "rawdict" variants of :meth:`Page.getText` has been ported to C which has greatly improved their performance. This improvement is mostly noticeable with text-oriented documents, where they now should execute almost two times faster.

* **Fixed** issue #369 ("mupdf: cmsCreateTransform failed") by removing ICC colorspace support.
* **Changed** :meth:`Page.getText` to accept additional keywords "blocks" and "words". These will deliver the results of :meth:`Page.getTextBlocks` and :meth:`Page.getTextWords`, respectively. So all text extraction methods are now available via a uniform API. Correspondingly, there are now new methods :meth:`TextPage.extractBLOCKS` and :meth:`TextPage.extractWords`.
* **Changed** :meth:`Page.getText` to default bit indicator *TEXT_INHIBIT_SPACES* to **off**. Insertion of additional spaces is **not suppressed** by default.

------

**Changes in Version 1.16.2**

* **Changed** text extraction methods of :ref:`Page` to allow detail control of the amount of extracted data.
* **Added** :meth:`planish_line` which maps a given line (defined as a pair of points) to the x-axis.
* **Fixed** an issue (w/o Github number) which brought down the interpreter when encountering certain non-UTF-8 encodable characters while using :meth:`Page.getText` with te "dict" option.
* **Fixed** issue #362 ("Memory Leak with getText('rawDICT')").

------

**Changes in Version 1.16.1**

* **Added** property :attr:`Quad.is_convex` which checks whether a line is contained in the quad if it connects two points of it.
* **Changed** :meth:`Document.insert_pdf` to now allow dropping or including links and annotations independently during the copy. Fixes issue #352 ("Corrupt PDF data and ..."), which seemed to intermittently occur when using the method for some problematic PDF files.
* **Fixed** a bug which, in matrix division using the syntax *"m1/m2"*, caused matrix *"m1"* to be **replaced** by the result instead of delivering a new matrix.
* **Fixed** issue #354 ("SyntaxWarning with Python 3.8"). We now always use *"=="* for literals (instead of the *"is"* Python keyword).
* **Fixed** issue #353 ("mupdf version check"), to no longer refuse the import when there are only patch level deviations from MuPDF.



------

**Changes in Version 1.16.0**

This major new version of MuPDF comes with several nice new or changed features. Some of them imply programming API changes, however. This is a synopsis of what has changed:

* PDF document encryption and decryption is now **fully supported**. This includes setting **permissions**, **passwords** (user and owner passwords) and the desired encryption method.
* In response to the new encryption features, PyMuPDF returns an integer (ie. a combination of bits) for document permissions, and no longer a dictionary.
* Redirection of MuPDF errors and warnings is now natively supported. PyMuPDF redirects error messages from MuPDF to *sys.stderr* and no longer buffers them. Warnings continue to be buffered and will not be displayed. Functions exist to access and reset the warnings buffer.
* Annotations are now **only supported for PDF**.
* Annotations and widgets (form fields) are now **separate object chains** on a page (although widgets technically still **are** PDF annotations). This means, that you will **never encounter widgets** when using :attr:`Page.firstAnnot` or :meth:`Annot.next`. You must use :attr:`Page.firstWidget` and :meth:`Widget.next` to access form fields.
* As part of MuPDF's changes regarding widgets, only the following four fonts are supported, when **adding** or **changing** form fields: **Courier, Helvetica, Times-Roman** and **ZapfDingBats**.

List of change details:

* **Added** :meth:`Document.can_save_incrementally` which checks conditions that are preventing use of option *incremental=True* of :meth:`Document.save`.
* **Added** :attr:`Page.firstWidget` which points to the first field on a page.
* **Added** :meth:`Page.getImageBbox` which returns the rectangle occupied by an image shown on the page.
* **Added** :meth:`Annot.setName` which lets you change the (icon) name field.
* **Added** outputting the text color in :meth:`Page.getText`: the *"dict"*, *"rawdict"* and *"xml"* options now also show the color in sRGB format.
* **Changed** :attr:`Document.permissions` to now contain an integer of bool indicators -- was a dictionary before.
* **Changed** :meth:`Document.save`, :meth:`Document.write`, which now fully support password-based decryption and encryption of PDF files.
* **Changed the names of all Python constants** related to annotations and widgets. Please make sure to consult the **Constants and Enumerations** chapter if your script is dealing with these two classes. This decision goes back to the dropped support for non-PDF annotations. The **old names** (starting with "ANNOT_*" or "WIDGET_*") will be available as deprecated synonyms.
* **Changed** font support for widgets: only *Cour* (Courier), *Helv* (Helvetica, default), *TiRo* (Times-Roman) and *ZaDb* (ZapfDingBats) are accepted when **adding or changing** form fields. Only the plain versions are possible -- not their italic or bold variations. **Reading** widgets, however will show its original font.
* **Changed** the name of the warnings buffer to :meth:`Tools.mupdf_warnings` and the function to empty this buffer is now called :meth:`Tools.reset_mupdf_warnings`.
* **Changed** :meth:`Page.getPixmap`, :meth:`Document.get_page_pixmap`: a new bool argument *annots* can now be used to **suppress the rendering of annotations** on the page.
* **Changed** :meth:`Page.add_file_annot` and :meth:`Page.add_text_annot` to enable setting an icon.
* **Removed** widget-related methods and attributes from the :ref:`Annot` object.
* **Removed** :ref:`Document` attributes *openErrCode*, *openErrMsg*, and :ref:`Tools` attributes / methods *stderr*, *reset_stderr*, *stdout*, and *reset_stdout*.
* **Removed** **thirdparty zlib** dependency in PyMuPDF: there are now compression functions available in MuPDF. Source installers of PyMuPDF may now omit this extra installation step.

**No version published for MuPDF v1.15.0**


------

**Changes in Version 1.14.20 / 1.14.21**

* **Changed** text marker annotations to support multiple rectangles / quadrilaterals. This fixes issue #341 ("Question : How to addhighlight so that a string spread across more than a line is covered by one highlight?") and similar (#285).
* **Fixed** issue #331 ("Importing PyMuPDF changes warning filtering behaviour globally").


------

**Changes in Version 1.14.19**

* **Fixed** issue #319 ("InsertText function error when use custom font").
* **Added** new method :meth:`Document.get_sigflags` which returns information on whether a PDF is signed. Resolves issue #326 ("How to detect signature in a form pdf?").


------

**Changes in Version 1.14.17**

* **Added** :meth:`Document.fullcopyPage` to make full page copies within a PDF (not just copied references as :meth:`Document.copyPage` does).
* **Changed** :meth:`Page.getPixmap`, :meth:`Document.get_page_pixmap` now use *alpha=False* as default.
* **Changed** text extraction: the span dictionary now (again) contains its rectangle under the *bbox* key.
* **Changed** :meth:`Document.movePage` and :meth:`Document.copyPage` to use direct functions instead of wrapping :meth:`Document.select` -- similar to :meth:`Document.delete_page` in v1.14.16.

------

**Changes in Version 1.14.16**

* **Changed** :ref:`Document` methods around PDF */EmbeddedFiles* to no longer use MuPDF's "portfolio" functions. That support will be dropped in MuPDF v1.15 -- therefore another solution was required.
* **Changed** :meth:`Document.embfile_Count` to be a function (was an attribute).
* **Added** new method :meth:`Document.embfile_Names` which returns a list of names of embedded files.
* **Changed** :meth:`Document.delete_page` and :meth:`Document.delete_pages` to internally no longer use :meth:`Document.select`, but instead use functions to perform the deletion directly. As it has turned out, the :meth:`Document.select` method yields invalid outline trees (tables of content) for very complex PDFs and sophisticated use of annotations.


------

**Changes in Version 1.14.15**

* **Fixed** issues #301 ("Line cap and Line join"), #300 ("How to draw a shape without outlines") and #298 ("utils.updateRect exception"). These bugs pertain to drawing shapes with PyMuPDF. Drawing shapes without any border is fully supported. Line cap styles and line line join style are now differentiated and support all possible PDF values (0, 1, 2) instead of just being a bool. The previous parameter *roundCap* is deprecated in favor of *lineCap* and *lineJoin* and will be deleted in the next release.
* **Fixed** issue #290 ("Memory Leak with getText('rawDICT')"). This bug caused memory not being (completely) freed after invoking the "dict", "rawdict" and "json" versions of :meth:`Page.getText`.


------

**Changes in Version 1.14.14**

* **Added** new low-level function :meth:`ImageProperties` to determine a number of characteristics for an image.
* **Added** new low-level function :meth:`Document.is_stream`, which checks whether an object is of stream type.
* **Changed** low-level functions :meth:`Document._getXrefString` and :meth:`Document._getTrailerString` now by default return object definitions in a formatted form which makes parsing easy.

------

**Changes in Version 1.14.13**

* **Changed** methods working with binary input: while ever supporting bytes and bytearray objects, they now also accept *io.BytesIO* input, using their *getvalue()* method. This pertains to document creation, embedded files, FileAttachment annotations, pixmap creation and others. Fixes issue #274 ("Segfault when using BytesIO as a stream for insertImage").
* **Fixed** issue #278 ("Is insertImage(keep_proportion=True) broken?"). Images are now correctly presented when keeping aspect ratio.


------

**Changes in Version 1.14.12**

* **Changed** the draw methods of :ref:`Page` and :ref:`Shape` to support not only RGB, but also GRAY and CMYK colorspaces. This solves issue #270 ("Is there a way to use CMYK color to draw shapes?"). This change also applies to text insertion methods of :ref:`Shape`, resp. :ref:`Page`.
* **Fixed** issue #269 ("AttributeError in Document.insert_page()"), which occurred when using :meth:`Document.insert_page` with text insertion.


------

**Changes in Version 1.14.11**

* **Changed** :meth:`Page.show_pdf_page` to always position the source rectangle centered in the target. This method now also supports **rotation by arbitrary angles**. The argument *reuse_xref* has been deprecated: prevention of duplicates is now **handled internally**.
* **Changed** :meth:`Page.insertImage` to support rotated display of the image and keeping the aspect ratio. Only rotations by multiples of 90 degrees are supported here.
* **Fixed** issue #265 ("TypeError: insertText() got an unexpected keyword argument 'idx'"). This issue only occurred when using :meth:`Document.insert_page` with also inserting text.

------

**Changes in Version 1.14.10**

* **Changed** :meth:`Page.show_pdf_page` to support rotation of the source rectangle. Fixes #261 ("Cannot rotate insterted pages").
* **Fixed** a bug in :meth:`Page.insertImage` which prevented insertion of multiple images provided as streams.


------

**Changes in Version 1.14.9**

* **Added** new low-level method :meth:`Document._getTrailerString`, which returns the trailer object of a PDF. This is much like :meth:`Document._getXrefString` except that the PDF trailer has no / needs no :data:`xref` to identify it.
* **Added** new parameters for text insertion methods. You can now set stroke and fill colors of glyphs (text characters) independently, as well as the thickness of the glyph border. A new parameter *render_mode* controls the use of these colors, and whether the text should be visible at all.
* **Fixed** issue #258 ("Copying image streams to new PDF without size increase"): For JPX images embedded in a PDF, :meth:`Document.extractImage` will now return them in their original format. Previously, the MuPDF base library was used, which returns them in PNG format (entailing a massive size increase).
* **Fixed** issue #259 ("Morphing text to fit inside rect"). Clarified use of :meth:`get_text_length` and removed extra line breaks for long words.

------

**Changes in Version 1.14.8**

* **Added** :meth:`Pixmap.set_rect` to change the pixel values in a rectangle. This is also an alternative to setting the color of a complete pixmap (:meth:`Pixmap.clear_with`).
* **Fixed** an image extraction issue with JBIG2 (monochrome) encoded PDF images. The issue occurred in :meth:`Page.getText` (parameters "dict" and "rawdict") and in :meth:`Document.extractImage` methods.
* **Fixed** an issue with not correctly clearing a non-alpha :ref:`Pixmap` (:meth:`Pixmap.clear_with`).
* **Fixed** an issue with not correctly inverting colors of a non-alpha :ref:`Pixmap` (:meth:`Pixmap.invert_irect`).

------

**Changes in Version 1.14.7**

* **Added** :meth:`Pixmap.set_pixel` to change one pixel value.
* **Added** documentation for image conversion in the :ref:`FAQ`.
* **Added** new function :meth:`get_text_length` to determine the string length for a given font.
* **Added** Postscript image output (changed :meth:`Pixmap.save` and :meth:`Pixmap.tobytes`).
* **Changed** :meth:`Pixmap.save` and :meth:`Pixmap.tobytes` to ensure valid combinations of colorspace, alpha and output format.
* **Changed** :meth:`Pixmap.save`: the desired format is now inferred from the filename.
* **Changed** FreeText annotations can now have a transparent background - see :meth:`Annot.update`.

------

**Changes in Version 1.14.5**

* **Changed:** :ref:`Shape` methods now strictly use the transformation matrix of the :ref:`Page` -- instead of "manually" calculating locations.
* **Added** method :meth:`Pixmap.pixel` which returns the pixel value (a list) for given pixel coordinates.
* **Added** method :meth:`Pixmap.tobytes` which returns a bytes object representing the pixmap in a variety of formats. Previously, this could be done for PNG outputs only (:meth:`Pixmap.tobytes`).
* **Changed:** output of methods :meth:`Pixmap.save` and (the new) :meth:`Pixmap.tobytes` may now also be PSD (Adobe Photoshop Document).
* **Added** method :meth:`Shape.drawQuad` which draws a :ref:`Quad`. This actually is a shorthand for a :meth:`Shape.drawPolyline` with the edges of the quad.
* **Changed** method :meth:`Shape.drawOval`: the argument can now be **either** a rectangle (:data:`rect_like`) **or** a quadrilateral (:data:`quad_like`).

------

**Changes in Version 1.14.4**

* **Fixes** issue #239 "Annotation coordinate consistency".


------

**Changes in Version 1.14.3**

This patch version contains minor bug fixes and CJK font output support.

* **Added** support for the four CJK fonts as PyMuPDF generated text output. This pertains to methods :meth:`Page.insertFont`, :meth:`Shape.insertText`, :meth:`Shape.insertTextbox`, and corresponding :ref:`Page` methods. The new fonts are available under "reserved" fontnames "china-t" (traditional Chinese), "china-s" (simplified Chinese), "japan" (Japanese), and "korea" (Korean).
* **Added** full support for the built-in fonts 'Symbol' and 'Zapfdingbats'.
* **Changed:** The 14 standard fonts can now each be referenced by a 4-letter abbreviation.

------

**Changes in Version 1.14.1**

This patch version contains minor performance improvements.

* **Added** support for :ref:`Document` filenames given as *pathlib* object by using the Python *str()* function.


------

**Changes in Version 1.14.0**

To support MuPDF v1.14.0, massive changes were required in PyMuPDF -- most of them purely technical, with little visibility to developers. But there are also quite a lot of interesting new and improved features. Following are the details:

* **Added** "ink" annotation.
* **Added** "rubber stamp" annotation.
* **Added** "squiggly" text marker annotation.
* **Added** new class :ref:`Quad` (quadrilateral or tetragon) -- which represents a general four-sided shape in the plane. The special subtype of rectangular, non-empty tetragons is used in text marker annotations and as returned objects in text search methods.
* **Added** a new option "decrypt" to :meth:`Document.save` and :meth:`Document.write`. Now you can **keep encryption** when saving a password protected PDF.
* **Added** suppression and redirection of unsolicited messages issued by the underlying C-library MuPDF. Consult :ref:`RedirectMessages` for details.
* **Changed:** Changes to annotations now **always require** :meth:`Annot.update` to become effective.
* **Changed** free text annotations to support the full Latin character set and range of appearance options.
* **Changed** text searching, :meth:`Page.searchFor`, to optionally return :ref:`Quad` instead :ref:`Rect` objects surrounding each search hit.
* **Changed** plain text output: we now add a *\n* to each line if it does not itself end with this character.
* **Fixed** issue 211 ("Something wrong in the doc").
* **Fixed** issue 213 ("Rewritten outline is displayed only by mupdf-based applications").
* **Fixed** issue 214 ("PDF decryption GONE!").
* **Fixed** issue 215 ("Formatting of links added with pyMuPDF").
* **Fixed** issue 217 ("extraction through json is failing for my pdf").

Behind the curtain, we have changed the implementation of geometry objects: they now purely exist in Python and no longer have "shadow" twins on the C-level (in MuPDF). This has improved processing speed in that area by more than a factor of two.

Because of the same reason, most methods involving geometry parameters now also accept the corresponding Python sequence. For example, in method *"page.show_pdf_page(rect, ...)"* parameter *rect* may now be any :data:`rect_like` sequence.

We also invested considerable effort to further extend and improve the :ref:`FAQ` chapter.


------

**Changes in Version 1.13.19**

This version contains some technical / performance improvements and bug fixes.

* **Changed** memory management: for Python 3 builds, Python memory management is exclusively used across all C-level code (i.e. no more native *malloc()* in MuPDF code or PyMuPDF interface code). This leads to improved memory usage profiles and also some runtime improvements: we have seen > 2% shorter runtimes for text extractions and pixmap creations (on Windows machines only to date).
* **Fixed** an error occurring in Python 2.7, which crashed the interpreter when using :meth:`TextPage.extractRAWDICT` (= *Page.getText("rawdict")*).
* **Fixed** an error occurring in Python 2.7, when creating link destinations.
* **Extended** the :ref:`FAQ` chapter with more examples.

------

**Changes in Version 1.13.18**

* **Added** method :meth:`TextPage.extractRAWDICT`, and a corresponding new string parameter "rawdict" to method :meth:`Page.getText`. It extracts text and images from a page in Python *dict* form like :meth:`TextPage.extractDICT`, but with the detail level of :meth:`TextPage.extractXML`, which is position information down to each single character.

------

**Changes in Version 1.13.17**

* **Fixed** an error that intermittently caused an exception in :meth:`Page.show_pdf_page`, when pages from many different source PDFs were shown.
* **Changed** method :meth:`Document.extractImage` to now return more meta information about the extracted imgage. Also, its performance has been greatly improved. Several demo scripts have been changed to make use of this method.
* **Changed** method :meth:`Document._getXrefStream` to now return *None* if the object is no stream and no longer raise an exception if otherwise.
* **Added** method :meth:`Document._deleteObject` which deletes a PDF object identified by its :data:`xref`. Only to be used by the experienced PDF expert.
* **Added** a method :meth:`paper_rect` which returns a :ref:`Rect` for a supplied paper format string. Example: *fitz.paper_rect("letter") = fitz.Rect(0.0, 0.0, 612.0, 792.0)*.
* **Added** a :ref:`FAQ` chapter to this document.

------

**Changes in Version 1.13.16**

* **Added** support for correctly setting transparency (opacity) for certain annotation types.
* **Added** a tool property (:attr:`Tools.fitz_config`) showing the configuration of this PyMuPDF version.
* **Fixed** issue #193 ('insertText(overlay=False) gives "cannot resize a buffer with shared storage" error') by avoiding read-only buffers.

------

**Changes in Version 1.13.15**

* **Fixed** issue #189 ("cannot find builtin CJK font"), so we are supporting builtin CJK fonts now (CJK = China, Japan, Korea). This should lead to correctly generated pixmaps for documents using these languages. This change has consequences for our binary file size: it will now range between 8 and 10 MB, depending on the OS.
* **Fixed** issue #191 ("Jupyter notebook kernel dies after ca. 40 pages"), which occurred when modifying the contents of an annotation.

------

**Changes in Version 1.13.14**

This patch version contains several improvements, mainly for annotations.

* **Changed** :attr:`Annot.lineEnds` is now a list of two integers representing the line end symbols. Previously was a *dict* of strings.
* **Added** support of line end symbols for applicable annotations. PyMuPDF now can generate these annotations including the line end symbols.
* **Added** :meth:`Annot.setLineEnds` adds line end symbols to applicable annotation types ('Line', 'PolyLine', 'Polygon').
* **Changed** technical implementation of :meth:`Page.insertImage` and :meth:`Page.show_pdf_page`: they now create there own contents objects, thereby avoiding changes of potentially large streams with consequential compression / decompression efforts and high change volumes with incremental updates.

------

**Changes in Version 1.13.13**

This patch version contains several improvements for embedded files and file attachment annotations.

* **Added** :meth:`Document.embfile_Upd` which allows changing **file content and metadata** of an embedded file. It supersedes the old method :meth:`Document.embfile_SetInfo` (which will be deleted in a future version). Content is automatically compressed and metadata may be unicode.
* **Changed** :meth:`Document.embfile_Add` to now automatically compress file content. Accompanying metadata can now be unicode (had to be ASCII in the past).
* **Changed** :meth:`Document.embfile_Del` to now automatically delete **all entries** having the supplied identifying name. The return code is now an integer count of the removed entries (was *None* previously).
* **Changed** embedded file methods to now also accept or show the PDF unicode filename as additional parameter *ufilename*.
* **Added** :meth:`Page.add_file_annot` which adds a new file attachment annotation.
* **Changed** :meth:`Annot.fileUpd` (file attachment annot) to now also accept the PDF unicode *ufilename* parameter. The description parameter *desc* correctly works with unicode. Furthermore, **all** parameters are optional, so metadata may be changed without also replacing the file content.
* **Changed** :meth:`Annot.fileInfo` (file attachment annot) to now also show the PDF unicode filename as parameter *ufilename*.
* **Fixed** issue #180 ("page.getText(output='dict') return invalid bbox") to now also work for vertical text.
* **Fixed** issue #185 ("Can't render the annotations created by PyMuPDF"). The issue's cause was the minimalistic MuPDF approach when creating annotations. Several annotation types have no */AP* ("appearance") object when created by MuPDF functions. MuPDF, SumatraPDF and hence also PyMuPDF cannot render annotations without such an object. This fix now ensures, that an appearance object is always created together with the annotation itself. We still do not support line end styles.

------

**Changes in Version 1.13.12**

* **Fixed** issue #180 ("page.getText(output='dict') return invalid bbox"). Note that this is a circumvention of an MuPDF error, which generates zero-height character rectangles in some cases. When this happens, this fix ensures a bbox height of at least fontsize.
* **Changed** for ListBox and ComboBox widgets, the attribute list of selectable values has been renamed to :attr:`Widget.choice_values`.
* **Changed** when adding widgets, any missing of the :ref:`Base-14-Fonts` is automatically added to the PDF. Widget text fonts can now also be chosen from existing widget fonts. Any specified field values are now honored and lead to a field with a preset value.
* **Added** :meth:`Annot.updateWidget` which allows changing existing form fields -- including the field value.

------

**Changes in Version 1.13.11**

While the preceeding patch subversions only contained various fixes, this version again introduces major new features:

* **Added** basic support for PDF widget annotations. You can now add PDF form fields of types Text, CheckBox, ListBox and ComboBox. Where necessary, the PDF is tranformed to a Form PDF with the first added widget.
* **Fixed** issues #176 ("wrong file embedding"), #177 ("segment fault when invoking page.getText()")and #179 ("Segmentation fault using page.getLinks() on encrypted PDF").


------

**Changes in Version 1.13.7**

* **Added** support of variable page sizes for reflowable documents (e-books, HTML, etc.): new parameters *rect* and *fontsize* in :ref:`Document` creation (open), and as a separate method :meth:`Document.layout`.
* **Added** :ref:`Annot` creation of many annotations types: sticky notes, free text, circle, rectangle, line, polygon, polyline and text markers.
* **Added** support of annotation transparency (:attr:`Annot.opacity`, :meth:`Annot.setOpacity`).
* **Changed** :attr:`Annot.vertices`: point coordinates are now grouped as pairs of floats (no longer as separate floats).
* **Changed** annotation colors dictionary: the two keys are now named *"stroke"* (formerly *"common"*) and *"fill"*.
* **Added** :attr:`Document.isDirty` which is *True* if a PDF has been changed in this session. Reset to *False* on each :meth:`Document.save` or :meth:`Document.write`.

------

**Changes in Version 1.13.6**

* Fix #173: for memory-resident documents, ensure the stream object will not be garbage-collected by Python before document is closed.

------

**Changes in Version 1.13.5**

* New low-level method :meth:`Page._setContents` defines an object given by its :data:`xref` to serve as the :data:`contents` object.
* Changed and extended PDF form field support: the attribute *widget_text* has been renamed to :attr:`Annot.widget_value`. Values of all form field types (except signatures) are now supported. A new attribute :attr:`Annot.widget_choices` contains the selectable values of listboxes and comboboxes. All these attributes now contain *None* if no value is present.

------

**Changes in Version 1.13.4**

* :meth:`Document.convertToPDF` now supports page ranges, reverted page sequences and page rotation. If the document already is a PDF, an exception is raised.
* Fixed a bug (introduced with v1.13.0) that prevented :meth:`Page.insertImage` for transparent images.

------

**Changes in Version 1.13.3**

Introduces a way to convert **any MuPDF supported document** to a PDF. If you ever wanted PDF versions of your XPS, EPUB, CBZ or FB2 files -- here is a way to do this.

* :meth:`Document.convertToPDF` returns a Python *bytes* object in PDF format. Can be opened like normal in PyMuPDF, or be written to disk with the *".pdf"* extension.

------

**Changes in Version 1.13.2**

The major enhancement is PDF form field support. Form fields are annotations of type *(19, 'Widget')*. There is a new document method to check whether a PDF is a form. The :ref:`Annot` class has new properties describing field details.

* :attr:`Document.is_form_pdf` is true if object type */AcroForm* and at least one form field exists.
* :attr:`Annot.widget_type`, :attr:`Annot.widget_text` and :attr:`Annot.widget_name` contain the details of a form field (i.e. a "Widget" annotation).

------

**Changes in Version 1.13.1**

* :meth:`TextPage.extractDICT` is a new method to extract the contents of a document page (text and images). All document types are supported as with the other :ref:`TextPage` *extract*()* methods. The returned object is a dictionary of nested lists and other dictionaries, and **exactly equal** to the JSON-deserialization of the old :meth:`TextPage.extractJSON`. The difference is that the result is created directly -- no JSON module is used. Because the user needs no JSON module to interpet the information, it should be easier to use, and also have a better performance, because it contains images in their original **binary format** -- they need not be base64-decoded.
* :meth:`Page.getText` correspondingly supports the new parameter value *"dict"* to invoke the above method.
* :meth:`TextPage.extractJSON` (resp. *Page.getText("json")*) is still supported for convenience, but its use is expected to decline.

------

**Changes in Version 1.13.0**

This version is based on MuPDF v1.13.0. This release is "primarily a bug fix release".

In PyMuPDF, we are also doing some bug fixes while introducing minor enhancements. There only very minimal changes to the user's API.

* :ref:`Document` construction is more flexible: the new *filetype* parameter allows setting the document type. If specified, any extension in the filename will be ignored. More completely addresses `issue #156 <https://github.com/pymupdf/PyMuPDF/issues/156>`_. As part of this, the documentation has been reworked.

* Changes to :ref:`Pixmap` constructors:
    - Colorspace conversion no longer allows dropping the alpha channel: source and target **alpha will now always be the same**. We have seen exceptions and even interpreter crashes when using *alpha = 0*.
    - As a replacement, the simple pixmap copy lets you choose the target alpha.

* :meth:`Document.save` again offers the full garbage collection range 0 thru 4. Because of a bug in :data:`xref` maintenance, we had to temporarily enforce *garbage > 1*. Finally resolves `issue #148 <https://github.com/pymupdf/PyMuPDF/issues/148>`_.

* :meth:`Document.save` now offers to "prettify" PDF source via an additional argument.
* :meth:`Page.insertImage` has the additional *stream* \-parameter, specifying a memory area holding an image.

* Issue with garbled PNGs on Linux systems has been resolved (`"Problem writing PNG" #133) <https://github.com/pymupdf/PyMuPDF/issues/133>`_.


------

**Changes in Version 1.12.4**

This is an extension of 1.12.3.

* Fix of `issue #147 <https://github.com/pymupdf/PyMuPDF/issues/147>`_: methods :meth:`Document.getPageFontlist` and :meth:`Document.getPageImagelist` now also show fonts and images contained in :data:`resources` nested via "Form XObjects".
* Temporary fix of `issue #148 <https://github.com/pymupdf/PyMuPDF/issues/148>`_: Saving to new PDF files will now automatically use *garbage = 2* if a lower value is given. Final fix is to be expected with MuPDF's next version. At that point we will remove this circumvention.
* Preventive fix of illegally using stencil / image mask pixmaps in some methods.
* Method :meth:`Document.getPageFontlist` now includes the encoding name for each font in the list.
* Method :meth:`Document.getPageImagelist` now includes the decode method name for each image in the list.

------

**Changes in Version 1.12.3**

This is an extension of 1.12.2.

* Many functions now return *None* instead of *0*, if the result has no other meaning than just indicating successful execution (:meth:`Document.close`, :meth:`Document.save`, :meth:`Document.select`, :meth:`Pixmap.save` and many others).

------

**Changes in Version 1.12.2**

This is an extension of 1.12.1.

* Method :meth:`Page.show_pdf_page` now accepts the new *clip* argument. This specifies an area of the source page to which the display should be restricted.

* New :attr:`Page.CropBox` and :attr:`Page.MediaBox` have been included for convenience.


------

**Changes in Version 1.12.1**

This is an extension of version 1.12.0.

* New method :meth:`Page.show_pdf_page` displays another's PDF page. This is a **vector** image and therefore remains precise across zooming. Both involved documents must be PDF.

* New method :meth:`Page.getSVGimage` creates an SVG image from the page. In contrast to the raster image of a pixmap, this is a vector image format. The return is a unicode text string, which can be saved in a *.svg* file.

* Method :meth:`Page.getTextBlocks` now accepts an additional bool parameter "images". If set to true (default is false), image blocks (metadata only) are included in the produced list and thus allow detecting areas with rendered images.

* Minor bug fixes.

* "text" result of :meth:`Page.getText` concatenates all lines within a block using a single space character. MuPDF's original uses "\\n" instead, producing a rather ragged output.

* New properties of :ref:`Page` objects :attr:`Page.MediaBoxSize` and :attr:`Page.CropBoxPosition` provide more information about a page's dimensions. For non-PDF files (and for most PDF files, too) these will be equal to :attr:`Page.rect.bottom_right`, resp. :attr:`Page.rect.top_left`. For example, class :ref:`Shape` makes use of them to correctly position its items.

------

**Changes in Version 1.12.0**

This version is based on and requires MuPDF v1.12.0. The new MuPDF version contains quite a number of changes -- most of them around text extraction. Some of the changes impact the programmer's API.

* :meth:`Outline.saveText` and :meth:`Outline.saveXML` have been deleted without replacement. You probably haven't used them much anyway. But if you are looking for a replacement: the output of :meth:`Document.get_toc` can easily be used to produce something equivalent.

* Class *TextSheet* does no longer exist.

* Text "spans" (one of the hierarchy levels of :ref:`TextPage`) no longer contain positioning information (i.e. no "bbox" key). Instead, spans now provide the font information for its text. This impacts our JSON output variant.

* HTML output has improved very much: it now creates valid documents which can be displayed by browsers to produce a similar view as the original document.

* There is a new output format XHTML, which provides text and images in a browser-readable format. The difference to HTML output is, that no effort is made to reproduce the original layout.

* All output formats of :meth:`Page.getText` now support creating complete, valid documents, by wrapping them with appropriate header and trailer information. If you are interested in using the HTML output, please make sure to read :ref:`HTMLQuality`.

* To support finding text positions, we have added special methods that don't need detours like :meth:`TextPage.extractJSON` or :meth:`TextPage.extractXML`: use :meth:`Page.getTextBlocks` or resp. :meth:`Page.getTextWords` to create lists of text blocks or resp. words, which are accompanied by their rectangles. This should be much faster than the standard text extraction methods and also avoids using additional packages for interpreting their output.


------

**Changes in Version 1.11.2**

This is an extension of v1.11.1.

* New :meth:`Page.insertFont` creates a PDF */Font* object and returns its object number.

* New :meth:`Document.extractFont` extracts the content of an embedded font given its object number.

* Methods **FontList(...)** items no longer contain the PDF generation number. This value never had any significance. Instead, the font file extension is included (e.g. "pfa" for a "PostScript Font for ASCII"), which is more valuable information.

* Fonts other than "simple fonts" (Type1) are now also supported.

* New options to change :ref:`Pixmap` size:

    * Method :meth:`Pixmap.shrink` reduces the pixmap proportionally in place.

    * A new :ref:`Pixmap` copy constructor allows scaling via setting target width and height.


------

**Changes in Version 1.11.1**

This is an extension of v1.11.0.

* New class *Shape*. It facilitates and extends the creation of image shapes on PDF pages. It contains multiple methods for creating elementary shapes like lines, rectangles or circles, which can be combined into more complex ones and be given common properties like line width or colors. Combined shapes are handled as a unit and e.g. be "morphed" together. The class can accumulate multiple complex shapes and put them all in the page's foreground or background -- thus also reducing the number of updates to the page's :data:`contents` object.

* All *Page* draw methods now use the new *Shape* class.

* Text insertion methods *insertText()* and *insertTextBox()* now support morphing in addition to text rotation. They have become part of the *Shape* class and thus allow text to be freely combined with graphics.

* A new *Pixmap* constructor allows creating pixmap copies with an added alpha channel. A new method also allows directly manipulating alpha values.

* Binary algebraic operations with geometry objects (matrices, rectangles and points) now generally also support lists or tuples as the second operand. You can add a tuple *(x, y)* of numbers to a :ref:`Point`. In this context, such sequences are called ":data:`point_like`" (resp. :data:`matrix_like`, :data:`rect_like`).

* Geometry objects now fully support in-place operators. For example, *p /= m* replaces point p with *p * 1/m* for a number, or *p * ~m* for a :data:`matrix_like` object *m*. Similarly, if *r* is a rectangle, then *r |= (3, 4)* is the new rectangle that also includes *fitz.Point(3, 4)*, and *r &= (1, 2, 3, 4)* is its intersection with *fitz.Rect(1, 2, 3, 4)*.

------

**Changes in Version 1.11.0**

This version is based on and requires MuPDF v1.11.

Though MuPDF has declared it as being mostly a bug fix version, one major new feature is indeed contained: support of embedded files -- also called portfolios or collections. We have extended PyMuPDF functionality to embrace this up to an extent just a little beyond the *mutool* utility as follows.

* The *Document* class now support embedded files with several new methods and one new property:

    - *embfile_Info()* returns metadata information about an entry in the list of embedded files. This is more than *mutool* currently provides: it shows all the information that was used to embed the file (not just the entry's name).
    - *embfile_Get()* retrieves the (decompressed) content of an entry into a *bytes* buffer.
    - *embfile_Add(...)* inserts new content into the PDF portfolio. We (in contrast to *mutool*) **restrict** this to entries with a **new name** (no duplicate names allowed).
    - *embfile_Del(...)* deletes an entry from the portfolio (function not offered in MuPDF).
    - *embfile_SetInfo()* -- changes filename or description of an embedded file.
    - *embfile_Count* -- contains the number of embedded files.

* Several enhancements deal with streamlining geometry objects. These are not connected to the new MuPDF version and most of them are also reflected in PyMuPDF v1.10.0. Among them are new properties to identify the corners of rectangles by name (e.g. *Rect.bottom_right*) and new methods to deal with set-theoretic questions like *Rect.contains(x)* or *IRect.intersects(x)*. Special effort focussed on supporting more "Pythonic" language constructs: *if x in rect ...* is equivalent to *rect.contains(x)*.

* The :ref:`Rect` chapter now has more background on empty amd infinite rectangles and how we handle them. The handling itself was also updated for more consistency in this area.

* We have started basic support for **generation** of PDF content:

    - *Document.insert_page()* adds a new page into a PDF, optionally containing some text.
    - *Page.insertImage()* places a new image on a PDF page.
    - *Page.insertText()* puts new text on an existing page

* For **FileAttachment** annotations, content and name of the attached file can extracted and changed.

------

**Changes in Version 1.10.0**

**MuPDF v1.10 Impact**

MuPDF version 1.10 has a significant impact on our bindings. Some of the changes also affect the API -- in other words, **you** as a PyMuPDF user.

* Link destination information has been reduced. Several properties of the *linkDest* class no longer contain valuable information. In fact, this class as a whole has been deleted from MuPDF's library and we in PyMuPDF only maintain it to provide compatibilty to existing code.

* In an effort to minimize memory requirements, several improvements have been built into MuPDF v1.10:

    - A new *config.h* file can be used to de-select unwanted features in the C base code. Using this feature we have been able to reduce the size of our binary *_fitz.o* / *_fitz.pyd* by about 50% (from 9 MB to 4.5 MB). When UPX-ing this, the size goes even further down to a very handy 2.3 MB.

    - The alpha (transparency) channel for pixmaps is now optional. Letting alpha default to *False* significantly reduces pixmap sizes (by 20% -- CMYK, 25% -- RGB, 50% -- GRAY). Many *Pixmap* constructors therefore now accept an *alpha* boolean to control inclusion of this channel. Other pixmap constructors (e.g. those for file and image input) create pixmaps with no alpha alltogether. On the downside, save methods for pixmaps no longer accept a *savealpha* option: this channel will always be saved when present. To minimize code breaks, we have left this parameter in the call patterns -- it will just be ignored.

* *DisplayList* and *TextPage* class constructors now **require the mediabox** of the page they are referring to (i.e. the *page.bound()* rectangle). There is no way to construct this information from other sources, therefore a source code change cannot be avoided in these cases. We assume however, that not many users are actually employing these rather low level classes explixitely. So the impact of that change should be minor.

**Other Changes compared to Version 1.9.3**

* The new :ref:`Document` method *write()* writes an opened PDF to memory (as opposed to a file, like *save()* does).
* An annotation can now be scaled and moved around on its page. This is done by modifying its rectangle.
* Annotations can now be deleted. :ref:`Page` contains the new method *deleteAnnot()*.
* Various annotation attributes can now be modified, e.g. content, dates, title (= author), border, colors.
* Method *Document.insert_pdf()* now also copies annotations of source pages.
* The *Pages* class has been deleted. As documents can now be accessed with page numbers as indices (like *doc[n] = doc.loadPage(n)*), and document object can be used as iterators, the benefit of this class was too low to maintain it. See the following comments.
* *loadPage(n)* / *doc[n]* now accept arbitrary integers to specify a page number, as long as *n < pageCount*. So, e.g. *doc[-500]* is always valid and will load page *(-500) % pageCount*.
* A document can now also be used as an iterator like this: *for page in doc: ...<do something with "page"> ...*. This will yield all pages of *doc* as *page*.
* The :ref:`Pixmap` method *getSize()* has been replaced with property *size*. As before *Pixmap.size == len(Pixmap)* is true.
* In response to transparency (alpha) being optional, several new parameters and properties have been added to :ref:`Pixmap` and :ref:`Colorspace` classes to support determining their characteristics.
* The :ref:`Page` class now contains new properties *firstAnnot* and *firstLink* to provide starting points to the respective class chains, where *firstLink* is just a mnemonic synonym to method *loadLinks()* which continues to exist. Similarly, the new property *rect* is a synonym for method *bound()*, which also continues to exist.
* :ref:`Pixmap` methods *samplesRGB()* and *samplesAlpha()* have been deleted because pixmaps can now be created without transparency.
* :ref:`Rect` now has a property *irect* which is a synonym of method *round()*. Likewise, :ref:`IRect` now has property *rect* to deliver a :ref:`Rect` which has the same coordinates as floats values.
* Document has the new method *searchPageFor()* to search for a text string. It works exactly like the corresponding *Page.searchFor()* with page number as additional parameter.


------

**Changes in Version 1.9.3**

This version is also based on MuPDF v1.9a. Changes compared to version 1.9.2:

* As a major enhancement, annotations are now supported in a similar way as links. Annotations can be displayed (as pixmaps) and their properties can be accessed.
* In addition to the document *select()* method, some simpler methods can now be used to manipulate a PDF:

    - *copyPage()* copies a page within a document.
    - *movePage()* is similar, but deletes the original.
    - *delete_page()* deletes a page
    - *delete_pages()* deletes a page range

* *rotation* or *setRotation()* access or change a PDF page's rotation, respectively.
* Available but undocumented before, :ref:`IRect`, :ref:`Rect`, :ref:`Point` and :ref:`Matrix` support the *len()* method and their coordinate properties can be accessed via indices, e.g. *IRect.x1 == IRect[2]*.
* For convenience, documents now support simple indexing: *doc.loadPage(n) == doc[n]*. The index may however be in range *-pageCount < n < pageCount*, such that *doc[-1]* is the last page of the document.

------

**Changes in Version 1.9.2**

This version is also based on MuPDF v1.9a. Changes compared to version 1.9.1:

* *fitz.open()* (no parameters) creates a new empty **PDF** document, i.e. if saved afterwards, it must be given a *.pdf* extension.
* :ref:`Document` now accepts all of the following formats (*Document* and *open* are synonyms):

  - *open()*,
  - *open(filename)* (equivalent to *open(filename, None)*),
  - *open(filetype, area)* (equivalent to *open(filetype, stream = area)*).

  Type of memory area *stream* may be *bytes* or *bytearray*. Thus, e.g. *area = open("file.pdf", "rb").read()* may be used directly (without first converting it to bytearray).
* New method *Document.insert_pdf()* (PDFs only) inserts a range of pages from another PDF.
* *Document* objects doc now support the *len()* function: *len(doc) == doc.pageCount*.
* New method *Document.getPageImageList()* creates a list of images used on a page.
* New method *Document.getPageFontList()* creates a list of fonts referenced by a page.
* New pixmap constructor *fitz.Pixmap(doc, xref)* creates a pixmap based on an opened PDF document and an :data:`xref` number of the image.
* New pixmap constructor *fitz.Pixmap(cspace, spix)* creates a pixmap as a copy of another one *spix* with the colorspace converted to *cspace*. This works for all colorspace combinations.
* Pixmap constructor *fitz.Pixmap(colorspace, width, height, samples)* now allows *samples* to also be *bytes*, not only *bytearray*.


------

**Changes in Version 1.9.1**

This version of PyMuPDF is based on MuPDF library source code version 1.9a published on April 21, 2016.

Please have a look at MuPDF's website to see which changes and enhancements are contained herein.

Changes in version 1.9.1 compared to version 1.8.0 are the following:

* New methods *get_area()* for both *fitz.Rect* and *fitz.IRect*
* Pixmaps can now be created directly from files using the new constructor *fitz.Pixmap(filename)*.
* The Pixmap constructor *fitz.Pixmap(image)* has been extended accordingly.
* *fitz.Rect* can now be created with all possible combinations of points and coordinates.
* PyMuPDF classes and methods now all contain  __doc__ strings,  most of them created by SWIG automatically. While the PyMuPDF documentation certainly is more detailed, this feature should help a lot when programming in Python-aware IDEs.
* A new document method of *getPermits()* returns the permissions associated with the current access to the document (print, edit, annotate, copy), as a Python dictionary.
* The identity matrix *fitz.Identity* is now **immutable**.
* The new document method *select(list)* removes all pages from a document that are not contained in the list. Pages can also be duplicated and re-arranged.
* Various improvements and new members in our demo and examples collections. Perhaps most prominently: *PDF_display* now supports scrolling with the mouse wheel, and there is a new example program *wxTableExtract* which allows to graphically identify and extract table data in documents.
* *fitz.open()* is now an alias of *fitz.Document()*.
* New pixmap method *tobytes()* which will return a bytearray formatted as a PNG image of the pixmap.
* New pixmap method *samplesRGB()* providing a *samples* version with alpha bytes stripped off (RGB colorspaces only).
* New pixmap method *samplesAlpha()* providing the alpha bytes only of the *samples* area.
* New iterator *fitz.Pages(doc)* over a document's set of pages.
* New matrix methods *invert()* (calculate inverted matrix), *concat()* (calculate matrix product), *pretranslate()* (perform a shift operation).
* New *IRect* methods *intersect()* (intersection with another rectangle), *translate()* (perform a shift operation).
* New *Rect* methods *intersect()* (intersection with another rectangle), *transform()* (transformation with a matrix), *include_point()* (enlarge rectangle to also contain a point), *include_rect()* (enlarge rectangle to also contain another one).
* Documented *Point.transform()* (transform a point with a matrix).
* *Matrix*, *IRect*, *Rect* and *Point* classes now support compact, algebraic formulations for manipulating such objects.
* Incremental saves for changes are possible now using the call pattern *doc.save(doc.name, incremental=True)*.
* A PDF's metadata can now be deleted, set or changed by document method *set_metadata()*. Supports incremental saves.
* A PDF's bookmarks (or table of contents) can now be deleted, set or changed with the entries of a list using document method *set_toc(list)*. Supports incremental saves.
