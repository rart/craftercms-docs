.. index:: Content Modeling, Modeling, Content Model

.. _content-modeling:

================
Content Modeling
================

Every content object in Crafter CMS is an object associated with a Content Model. Content Models allow you to add structure to your content and facilitate consumption via various visual representations or via APIs. One of the great things about Crafter CMS content models is that your content can be semi-structured which allows content authors the freedom to be as creative as they'd like to be, but provide the template/UI and API developers enough structure to produce solid multi-channel renditions of the content. This section will walk you through Content Type management in Crafter Studio to help you create the models that best fit your requirements.

-------------------------------
Content Types in Crafter Studio
-------------------------------

Content Type Management in Crafter Studio is located in the |siteConfig|.

.. image:: /_static/images/content-model/site-config-link.png
	:width: 40%
	:alt: Site Config Link
	:align: center

Content Types are limited to two core types: Pages and Components. Both are made up of three ingredients:

#. Model: The content pieces that will be captured from the content authors for the page or component
#. View: The view template that will render the content, typically to HTML markup
#. Controller: The controller that handles the incoming request for the page or component

^^^^^
Pages
^^^^^

Pages are top-level container types. Pages hold content, and optionally components. Content within pages is made up of various types, for example content can be a date, an image, or a rich text field.

^^^^^^^^^^
Components
^^^^^^^^^^

Components only differ from pages in that they can't render by themselves, instead, they must render within a container page or another component.

.. _content-model:

-----------------------------
Content Type Model Definition
-----------------------------
Content models are defined via Crafter Studio's graphical modeling tool under Content Types:

.. image:: /_static/images/content-model/content-type-management.png
	:width: 50%
	:alt: Site Config - Content Types
	:align: center

You can now either create a new content type or open an existing type. Creating a new content type brings up a dialog that requests some basic content type information.

.. image:: /_static/images/content-model/create-content-type-1.png
	:width: 40%
	:alt: Site Config - Create Content Type
	:align: center

You now specify:

* Display Label: The name of your new content type as you'll see it in Crafter Studio.
* Content Type Name: The low-level system name of your content type, this field will be automatically generated for you. Modify this only if you know what you're doing.
* Type: Choose if you're defining a Page or a Component.

.. note:: Content Type Name will be removed in a future release in favor of full automation of name generation with collision resolution mechanics.

.. _form-builder-basics:

^^^^^^^^^^^^^^^^^^^
Form Builder Basics
^^^^^^^^^^^^^^^^^^^

.. figure:: /_static/images/content-model/create-content-type-2.png
	:alt: Content Type Editor
	:align: center

Crafter Studio's Form Builder

+--------+---------------------------------------------------------------------------------------+
|| Label || Description                                                                          |
+--------+---------------------------------------------------------------------------------------+
|| 1     || Content Type Actions: Open Existing Content Type or Create a New Type.               |
+--------+---------------------------------------------------------------------------------------+
|| 2     || Form Builder: The begining of the form builder and it's headed by the name of the    |
||       || currently open Content Type.                                                         |
||       || Click here to explore the global properties of the type in the Properties Explorer,  |
||       || #3.                                                                                  |
+--------+---------------------------------------------------------------------------------------+
|| 3     || Properties Explorer: Helps configure the properties of the currently                 |
||       || selected item. Clicking on an item on the left side of the screen,                   |
||       || like #2 or #7 will populate this control and allow you to modify                     |
||       || the selected item.                                                                   |
+--------+---------------------------------------------------------------------------------------+
|| 4     || Form Controls: This is a list of available form controls for you to build your own   |
||       || form with. Note that the list has a scrollbar for many types of useful controls.     |
||       || Controls can be dragged from the controls list onto the form builder.                |
+--------+---------------------------------------------------------------------------------------+
|| 5     || Data Sources: Shows the list of available data sources that can be attached to this  |
||       || content type such that the content authors can pull content and incorporate it into  |
||       || pages or components. Data Sources can be dragged over to the form builder            |
||       || and configured as needed.                                                            |
||       || The content author will then use the control to pull data from that data source into |
||       || the content object.                                                                  |
+--------+---------------------------------------------------------------------------------------+
|| 6     || Form Section: Form sections help cluster a number of controls together to make it    |
||       || easier for content authors. Click on the form section to edit its properties in      |
||       || the Properties Explorer.                                                             |
+--------+---------------------------------------------------------------------------------------+
|| 7     || Form Canvas: Actual controls that have been placed on this form.                     |
||       || Clicking on a control will allow you to configure this control in the Properties     |
||       || Explorer.                                                                            |
+--------+---------------------------------------------------------------------------------------+
|| 8     || Data Source: The data sources configured for this content type.                      |
||       || To configure a data source, click on it and then edit the properties                 |
||       || in the Properties Explorer.                                                          |
+--------+---------------------------------------------------------------------------------------+
|| 9     || Save or Cancel the changes to the Content Type.                                      |
+--------+---------------------------------------------------------------------------------------+

^^^^^^^^^^^^^^^^^^^^^^^^^^^
Properties of Content Types
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Let's select the content type itself, by clicking on the content type name at the top of the Form Builder and explore its properties.

.. figure:: /_static/images/content-model/create-content-type-3.png
	:alt: Properties Explorer
	:align: center

The fields available at this level are:

+---------------+--------------------------------------------------------------------------------+
|| Field        || Description                                                                   |
+---------------+--------------------------------------------------------------------------------+
|| Title        || Content Type's friendly name                                                  |
+---------------+--------------------------------------------------------------------------------+
|| Description  || Description of the Content Type                                               |
+---------------+--------------------------------------------------------------------------------+
|| Object Type  || Page or Component (read only)                                                 |
+---------------+--------------------------------------------------------------------------------+
|| Content Type || System name and path of this content type (read only)                         |
+---------------+--------------------------------------------------------------------------------+
|| Preview      ||                                                                               |
|| Image        ||                                                                               |
+---------------+--------------------------------------------------------------------------------+
|| Configuration|| Contains config.xml which holds information about the content type such as the|
||              || limit where content can be created, is it previewable, etc.                   |
+---------------+--------------------------------------------------------------------------------+
|| Controller   ||                                                                               |
+---------------+--------------------------------------------------------------------------------+
|| Display      || View template to use when rendering this content                              |
|| Template     ||                                                                               |
+---------------+--------------------------------------------------------------------------------+
|| Merge        || The inheritance pattern to use with content of this type, please see Content  |
|| Strategy     || Inheritance for more detail on this feature :ref:`content-inheritance`        |
+---------------+--------------------------------------------------------------------------------+

The 2 key properties are: the display template (:ref:`content-view-templates`) which is the HTML template that renders the final Web page; the content inheritance (:ref:`content-inheritance`) which determines how this content type will inherit from parent XML files in the system.

.. _content-creation-permissions-section:

Content Creation Permissions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Limiting where a content type can be created is through the Configuration Property of a content type (config.xml) using the following tags:

.. code-block:: xml

    <paths>
        <includes>
            <pattern>REG_EXP_HERE</pattern>
        </includes>
    </paths>

OR

.. code-block:: xml

    <paths>
	    <excludes>
		    <pattern>REG_EXP_HERE</pattern>
	    </excludes>
    </paths>


You can only use one of either include or exclude. Use Include when you need to whitelist places, use exclude when you need to blacklist.

We'll look at an example of limiting where you can create content from the Website_Editorial blueprint that comes out of the box.

From the **Sidebar**, click on **Site Config** at the bottom.  Next, click on **Content Types** then either create a new content type or open an existing content type.  In the image below, we have the content type **Page - Article** open for editing.  Go to the **Properties Explorer** and click on **Configuration**.  A pencil will appear next to the file name *config.xml*, click on that pencil to edit.

.. figure:: /_static/images/content-model/form-engine-prop-configuration.png
    :alt: Form Engine Properties Configuration
	:align: center

To limit where this particular content type can be created, the tags, <paths><includes><pattern>some_regex_pattern</pattern></includes></paths> are included towards the bottom of the file.  Here, we can see that content type **Page - Article** can be created anywhere under */site/website/articles*

.. figure:: /_static/images/content-model/form-engine-prop-config-file.png
    :alt: Form Engine Properties Configuration File config.xml
    :align: center

.. code-block:: xml

    <paths>
		<includes>
			<pattern>^/site/website/articles/.*</pattern>
		</includes>
	</paths>

To see how the above tags/example works, go to the **Sidebar** and right click on the **Home** folder and select **New Content**.  Notice that content type **Page - Article** is not available from the content types listed.

.. figure:: /_static/images/content-model/form-engine-prop-config-sample-no.png
    :alt: Form Engine Properties Config File "Page - Articles" Not Available
    :align: center

From the **Sidebar** again, navigate from the **Pages** folder to the /Home/articles/2016/12/ folder then right click and select **New Content**, notice that the content type **Page - Article** is available from the list.

.. figure:: /_static/images/content-model/form-engine-prop-config-sample-yes.png
    :alt: Form Engine Properties Config File "Page - Articles" Available
    :align: center

To see more examples, try creating content types in the other folders in the **Sidebar** such as the **Taxonomy** folder, the **Components** folder and anywhere under the **Pages** folder.

.. _form-controls:

^^^^^^^^^^^^^
Form Controls
^^^^^^^^^^^^^

Form Controls are data input controls that, once placed on a form, will capture that input from the content authors and store it in the content object. Crafter CMS ships with a number of out-of-the-box controls and you can also create your own by reading :ref:`form-engine-control`.

.. figure:: /_static/images/content-model/form-engine-controls.png
    :alt: Form Engine Controls
	:align: center

Each Form Control type has it's own properties and constraints.  Some constraints are common, like "Variable Name" and "Required" while others apply only to the type, e.g. Height and Width limitations on the Image Picker control.  

Here's a list of available Form Engine Controls:

.. include:: form-controls/list-form-controls.rst

.. _form-control-variable-names:

^^^^^^^^^^^^^^^^^^^^^^^^^^^
Form Control Variable Names
^^^^^^^^^^^^^^^^^^^^^^^^^^^
Every Form Control has a Variable Name property.  The Variable Name is used by the form engine to store the content entered by the user in the content model and search index.  This same Variable Name is used later by templates and controllers to retrieve the value.

**Variable Name Best Practices**

#. Be descriptive.  Well thought out Variable Names help with template and controller readability.
#. Use camel case. Example: "productSummary".
#. Use regex constraints on input boxes to enforce additional validation rules
#. Do not use Reserved names.

**Reserved Variable Names**

The following variable names are used by Crafter CMS.
  
+-------------------+----------------------------------------------------------+
|| file-name        || Used by the File Name and Auto File Name control.       |
+-------------------+----------------------------------------------------------+
|| internal-name    || Used by Crafter Studio to label the content object      |
+-------------------+----------------------------------------------------------+
|| placeInNav       || Used by the Page Order control.                         |
+-------------------+----------------------------------------------------------+
|| disabled         || Used to logically remove an object in content delivery. |
+-------------------+----------------------------------------------------------+
|| expired          || Used to logically remove an object after date           |
+-------------------+----------------------------------------------------------+
|| objectId         || UUID. Auto assigned by Crafter                          |
+-------------------+----------------------------------------------------------+
|| objectGroupId    || First part of objectId. Auto assigned by Crafter        |
+-------------------+----------------------------------------------------------+
|| createdDate      || create date. Auto assigned by Crafter                   |
+-------------------+----------------------------------------------------------+
|| lastModifiedDate || Last modified date. Auto assigned by Crafter            |
+-------------------+----------------------------------------------------------+
|| content-type     || Content type name                                       |
+-------------------+----------------------------------------------------------+
|| display-template || Path to default template for type                       |
+-------------------+----------------------------------------------------------+
|| merge-strategy   || Crafter Core/Engine "Merge Strategy" for content type   |
+-------------------+----------------------------------------------------------+	 
|| id               || reserved by Solr                                        |
+-------------------+----------------------------------------------------------+


**Variable Names and Search Indexing**

Crafter CMS indexes your content in to Solr using your content model variable name as the Solr field name. 
Use the Solr schema to configure your Solr variable/solr field types in search.

To facilitate indexing to Solr, the following suffix should be appended to variable names depending on the variable data type:

+------------+---------+-------------+----------------------------------------------------+
||           || Field  || Multivalue || Description                                       |
|| Type      || Suffix || Suffix     ||                                                   |
||           ||        || (repeating ||                                                   |
||           ||        || groups)    ||                                                   |
+============+=========+=============+====================================================+
|| integer   || _i     || _is        || a 32 bit signed integer                           |
+------------+---------+-------------+----------------------------------------------------+
|| string    || _s     || _ss        || String (UTF-8 encoded string or Unicode). A string|
||           ||        ||            ||  value is indexed as a single unit.               |
+------------+---------+-------------+----------------------------------------------------+
|| long      || _l     || _ls        || a 64 bit signed integer                           |
+------------+---------+-------------+----------------------------------------------------+
|| text      || _t     || _txt       || Multiple words or tokens                          |
+------------+---------+-------------+----------------------------------------------------+
|| boolean   || _b     || _bs        || true or false                                     |
+------------+---------+-------------+----------------------------------------------------+
|| float     || _f     || _fs        || IEEE 32 bit floating point number                 |
+------------+---------+-------------+----------------------------------------------------+
|| double    || _d     || _ds        || IEEE 64 bit floating point number                 |
+------------+---------+-------------+----------------------------------------------------+
|| date      || _dt    || _dts       || A date in Solr's date format                      |
+------------+---------+-------------+----------------------------------------------------+
|| text with || _html  ||            ||                                                   |
|| html tags ||        ||            ||                                                   |
+------------+---------+-------------+----------------------------------------------------+

.. _data-sources:

^^^^^^^^^^^^
Data Sources
^^^^^^^^^^^^
.. index:: Data Sources

.. figure:: /_static/images/content-model/form-engine-data-sources.png
	:alt: Form Engine Data Sources
	:align: center

Data Sources are pickers that help pull in content from internal or external storage/systems. For example, data source include: desktop video uploader, desktop image uploader, and so on. Crafter CMS ships with a number of out-of-the-box data sources and you can also create your own by reading :ref:`form-engine-data-source`.

Form Engine Data Sources (please use the scrollbar to see more controls)

.. include:: form-sources/list-form-sources.rst

^^^^^^^^^^^
Form Canvas
^^^^^^^^^^^

The canvas is where the form actually gets built. The building process is perfomed by simply dragging the controls from the Form Controls over to the canvas, rearranging the controls in the order you'd like to present to the content authors, and configuring the controls individually.

Controls on the canvas are configured by clicking on the control, and then editing the control's configuration in the Properties Explorer, see item #3 in :ref:`form-builder-basics`. Different controls have different configuration, so please review the individual form control configuration listed in :ref:`form-controls`.

Two controls have a special significance to the form canvas: :ref:`form-section` and :ref:`form-repeating-group`. Form Section Control creates a form section that can be expanded and collapsed and holds within it other controls. This is typically used to group together controls that cover a similar concern and help provide the content authors with a clear and organized form when editing in form mode.
Like the Form Section Control, Repeating Group Control is also a container that holds other controls, but the purpose is to allow a set of controls to repeat as configured. This is typically used to allow content authors to enter a set of meta-data and repeat it as many times as desired and permitted by configuration.

The canvas allows the form-based content capture only, and is used by content authors when they're in that mode. In-Context Editing will leverage the form components, but not the canvas when authors are in that mode. Learn more about In-Context Editing configuration in :ref:`in-context-editing`.

.. _content-view-templates:

---------------------------
Content Type View Templates
---------------------------

View templates control how the model is rendered as HTML. Crafter uses `FreeMarker <http://freemarker.org>`_ as the templating engine, and provide the full model defined by the model in the previous section. Every element in the model is accessible to the view template via a simple API ``${contentModel.VARIABLE_NAME}`` where variable name is the ``Name / Variable Name`` definition in the Form Control. View templates are primarily written in HTML, backed by CSS with API calls weaved within to pull content from the primary Crafter CMS model or additional model (via APIs, please read :ref:`groovy-api` for that topic).

An example view template

.. code-block:: guess

	<#import "/templates/system/common/cstudio-support.ftl" as studio />

	<!DOCTYPE html>
	<html lang="en">
		<head>
	    		<!-- Basic Page Need
	    		================================================== -->
			<meta charset="utf-8">
			<title>${contentModel.browser_title}</title>
			<meta name="description" content="${contentModel.meta_description}">
			<meta name="keywords" content="${contentModel.meta_keywords}">
		</head>
		<body>
			<div class="body" <@studio.iceAttr iceGroup="body"/>>
				${contentModel.body_html}
			</div>

			<#if (contentModel.analytics_script)??>${contentModel.analytics_script}</#if>
		</body>
	</html>

The simple example renders a simple HTML page with a very basic model. Let's review the model first:

+-------------------+--------------+-------------------------------------------------------------+
|| Model Element    || Control     || Purpose                                                    |
+-------------------+--------------+-------------------------------------------------------------+
|| browser_title    || Input       || Provide a browser title for the page                       |
+-------------------+--------------+-------------------------------------------------------------+
|| meta_keywords    || Input       || SEO keywords associated with the page                      |
+-------------------+--------------+-------------------------------------------------------------+
|| body_html        || Rich Text   || The page's main HTML body (in this case, it's              |
||                  || Editor      || just a static HTML block).                                 |
+-------------------+--------------+-------------------------------------------------------------+
|| analytics_script || Text Area   || Analytics's Engine JavaScript                              |
+-------------------+--------------+-------------------------------------------------------------+

The `FreeMarker <http://freemarker.org>`_ language is supported. For detailed Freemarker documentation, please visit: `http://freemarker.org <http://freemarker.org>`_ 

.. _content-type-controller-definition:

----------------------------------
Content Type Controller Definition
----------------------------------

Crafter page and components can have their own controller scripts too, that are executed before the page or component
is rendered, and that can contribute to the model of the template. These scripts, besides the common variables, have
the ``templateModel`` and the ``contentModel`` available. The ``templateModel`` is the actual map model of the
template, and any variable put in it will be accessible directly in the template, eg. if the script has the line
``templateModel.var = 5``, then in the template the var's value can be printed with ``${var}``. The ``contentModel``
is the XML descriptor content, of type SiteItem. The scripts don't have to return any result, just populate the
``templateModel``.

There are 2 ways in which you can "bind" a script to a page or component:

#.  Put the script under Scripts > pages or Scripts > components, and name it after the page or component content type.
#.  When creating the content type for the page or component, add an Item Selector with the variable name ``scripts``. Later when creating
    a page or component of that type, you can select multiple scripts that will be associated to the page or component.

The following is an example of a component script. The component content type is ``/component/upcoming-events``. We can then place the
script in Scripts > components > upcoming-events.groovy so that it is executed for all components of that type.

.. code-block:: groovy

    import org.craftercms.engine.service.context.SiteContext

    import utils.DateUtils

    def now = DateUtils.formatDateAsIso(new Date())
    def queryStr = "crafterSite:\"${siteContext.siteName}\" AND content-type:\"/component/event\" AND disabled:\"false\" AND date_dt:[${now} TO *]"
    def start = 0
    def rows = 1000
    def sort = "date_dt asc"
    def query = searchService.createQuery()

    query.setQuery(queryStr)
    query.setStart(start)
    query.setRows(rows)
    query.addParam("sort", sort)
    query.addParam("fl", "localId")

    def events = []
    def searchResults = searchService.search(query)
    if (searchResults.response) {
        searchResults.response.documents.each {
            def event = [:]
            def item = siteItemService.getSiteItem(it.localId)

            event.image = item.image.text
            event.title = item.title_s.text
            event.date = DateUtils.parseModelValue(item.date_dt.text)
            event.summary = item.summary_html.text

            events.add(event)
        }
    }

    contentModel.events = events

You might notice that we're importing a ``utils.DateUtils`` class. This class is not part of Crafter CMS, but instead it is a Groovy class
specific to the site. To be able to use this class, you should place it under Classes > groovy > utils and name it DateUtils.groovy,
where everything after the groovy directory is part of the class' package. It's recommended for all Groovy classes to follow this
convention.

.. code-block:: groovy

    package utils

    import java.text.SimpleDateFormat

    class DateUtils {

        static def parseModelValue(value){
            def dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss")
                dateFormat.setTimeZone(TimeZone.getTimeZone("UTC"))
            return dateFormat.parse(value)
        }

        static def formatDateAsIso(date) {
            def dateFormat = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ss'Z'")
                dateFormat.setTimeZone(TimeZone.getTimeZone("UTC"))
            return dateFormat.format(date)
        }

    }

For more information on the FreeMarker (Templating) APIs, pleasee see :ref:`templating-api`.

For more information on the Groovy APIs, please see :ref:`groovy-api`

