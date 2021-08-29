# XSLT Introduction

## Aims

In this exercise, you will create a stylesheet to transform an XML file containing information about a training course. You will not use Mapforce, but rather you will hand craft the stylesheet. The more you know and understand about how XSLT Stylesheets work, the better you will be at working with Mapforce when generating XSLT stylesheet transformations.

## Part 1 Creating a basic stylesheet

1. Initially, you will review the XML document that contains the XML that you will be styling. Using XML Spy, open up 

[buildingEffectiveXMLApplications.xml](data/buildingEffectiveXMLApplications.xml)


2. Review the elements and attributes in the XML document.
3. Launch XML Spy. You will be using this tool to create your stylesheet. 
4. Select **File**, **New**, and then select **XSLT StylesheetVersion 2.0**.
5. Note that you are now presented with an XML document with the root element of `<xsl:stylesheet>`.
6. It is within these elements that you will add your templates.
7. Remove the `<xsl:output>` element from the document, since you will be creating HTML output. We could create XML just as easily as HTML but with HTML we can easily review out output and see if it is behaving as expected.

## Part 2 Adding a template

1. Within the `<xsl:stylesheet>` elements, add an `<xsl:template>` element, with a match attribute having the value of `course`.
2. Within the `<xsl:template>` tag, initially provide the basic skeleton HTML markup that will contain your HTML about the course. See below for an example:

```
<xsl:template match='course'>

<html>
    <head>
      <title></title>
    </head>
    <body>

    </body>
</html>

</xsl:template>
```

1. Within the title tag in the HTML, we want to output the title of the course. To output a value, use the `<xsl:value-of>` tag. Add this tag with a select attribute value set to title.
 You should then have the following:

```
<title><xsl:value-of select='title'/></title>
```

This will display the title of the course in the title bar of the Web browser when displayed in the browser.

1. Now you need to display some information about the course in the body of the Web page. Within the `<body>` elements, add some HTML markup to display the title of the course, the outline of the course, and the duration of the course. Format it how you wish. You could use `<h1>` elements for the title and `<p>` elements for the outline and duration if you wish.

## Part 3 Setting up an additional template

You will now add a template to display each chapter, and you will call this template from the template that you created in part 2.

1. Just before your closing `<xsl:stylesheet>` element, add an additional `template` element with the `match` attribute set to `chapter`.
2. Display the name of the chapter by using the `<xsl:value-of>` element as before, but this time, set the value to be `title`.
3. Add a `<br/>` tag to the end of the value-of element to add a line break.
4. You now need to call this template from the earlier template. Return to your previous template, and underneath where you displayed the duration of the course, add an `<xsl:apply-templates>` element, with a select value set to `contents/chapter`.

## Part 4 Linking and Testing your Stylesheet


1. Save your stylesheet somewhere on your machine.
2. Have the buildingEffectiveXMLApplications.xml open in XML Spy. 
3. From the menu, select **XSL** \ **Assign XSL**.
4. An XML Spy dialog box will ask if you want your XML to be **Pretty Printed**. This means that it will indent the XML in a readable fashion. Click **Yes**.
5. Browse to your stylesheet and select OK.
6. Now click on the browser view in XML Spy. You should see a transformed XML file! If it has not worked, fix the errors in the stylesheet before proceeding.

## Part 5 Stepping through a transformation with the XML Spy XSLT Debugger

In this section, you will work with the XSLT debugger, to examine what is happening when a stylesheet is being processed. You may also want to use the debugger in further exercises when things do not seem to be going to plan!

1. In XML Spy, whilst viewing the XML file **buildingEffectiveXMLApplications.xml**, from the menu, click **XSL**, and then click **Start Debugger**/**Go**.
2. You are now presented with 3 windows. The XML source tree is on the left, the stylesheet is in the middle (currently displaying what are the default templates), and the results tree is on the right (currently empty). 

Notice that the template that is initially highlighted in the centre pane is a template matching any element (\*) or the document object (/). This template will be invoked first. It is a default template, and it contains a child element `<apply-templates>`, so it will continue processing.

2. To step into this template, press F11, and you will see that it goes into apply templates. Press F11 again, and it will now go to the processing instruction at the top of the XML document. Note that there is another default template that matches this, so in the centre pane, it jumps to that template. Press F11 again until the `<course>` element is highlighted in the left pane.
3. Note that when the `<course>` is highlighted, it now jumps to your template matching the course. Keep pressing F11 to step into each process step, and see if you can make sense of what is taking place. Note that the results tree is now starting to be built up.
4. Keep pressing F11 until you are informed by a dialog that the debugger has finished. If you are unsure as to what is taking place at any time, ask your instructor for assistance.


## Part 6 (Optional) Modifying your Stylesheet

If you have time, experiment with your stylesheet. Try changing it to display the chapter objectives or the course objectives. You could also display the course code somewhere in the page. No detailed instructions are provided for this.

