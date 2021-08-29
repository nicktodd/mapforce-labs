# Chapter 2 XPath

## Aims

In this exercise, you will be working with more complex XPath expressions, learning to navigate the XML tree from within your stylesheet.

## Part 1 Working with XPath Expressions

1. You can either carry on working with your stylesheet from the previous exercise, or you can use the solution from the previous exercise. Either copy <LAB\_HOME>\Labs\XSLTIntro\courseOutline.xslt  or <LAB\_HOME>\Solutions\XSLTIntro\courseOutline.xslt into the <LAB\_HOME>\labs\XPath folder.
2. Using XML Spy, open up <LAB\_HOME>\labs\XPath\courseOutline.xslt.
3. Modify the first template so that it now matches on the root (/), rather than course.
4. Now modify the various XPath expressions within the template so that they still work.
5. Test your stylesheet with <LAB\_HOME>\labs\XPath\webServicesJava.xml to ensure that it still works. This is a different course, but it follows an identical structure to the one used in the previous chapter. If you are getting a blank screen, then you probably have incorrect XPath expressions.
6. Now add the child axis specifier to one of your XPath expressions, and test that it still works. Remember, child is the default axis.
7. Now revisit your template for each chapter, and if you have not added it already, add appropriate markup to display each of the chapter objectives.
8. Next to each chapter name, add a value-of element to display the total duration of the course. Although you would not do this in reality, it will test to see if you can use the parent axis. Try this with both the shorthand and longhand versions of the axis specifier. Test your stylesheet.

## Part 2 Working with predicates

1. You now want to make the first chapter come up in red. Create a template that will only match the first chapter. From within it, display the chapter title and objectives, but in a red font. Test your new template in the browser.
2. Now modify your stylesheet so the last objective of each chapter comes out in green. Hint: you can use the last() function in the predicate to identify if the node is the last one.
3. Finally, modify the stylesheet so that the first four chapters are in one colour, and the rest of the chapters are in a different colour.

## Part 3 (Optional) Experimenting with axes and predicates

If you have time, try experimenting with different axes and predicates, and attempt to predict your results before you view it in the XML Spy browser view.

# Chapter 3 XPath Functions

## Aims

In this exercise you will experiment with the various XPath functions to further control the output from an XSLT stylesheet.

## Part 1 Working with Functions

In this exercise you will be using as a basis your stylesheet from the exercise XSLT Introduction, _ **not** _ the previous exercise on XPath.

1. As you did at the start of the previous exercise, either copy <LAB\_HOME>\Labs\XSLTIntro\courseOutline.xslt  or <LAB\_HOME>\Solutions\XSLTIntro\courseOutline.xslt into the <LAB\_HOME>\labs\XPathFunctions folder.
2. Using XML Spy, open up <LAB\_HOME>\labs\XPathFunctions\courseOutline.xslt.
3. Link the stylesheet to the provided XML file called <LAB\_HOME>\labs\XPathFunctions\xmloverview.xml.
4. Now modify the stylesheet to display how many chapters are in the course just underneath where the duration is displayed.
5. Modify the chapter template so that the chapter number is also displayed. This is done using the <xsl:number> element. You can use an empty element for this, and place it immediately before where the title is displayed. Note that this is not an XPath function, but an XSL element. You should have something like the following in your chapter template:

<xsl:template match='chapter'>

<xsl:number/>. <xsl:value-of select='title'/><br/>

</xsl:template>

1. Test your stylesheet before continuing.
2. You will now calculate the average number of chapters delivered per day and display it just after where you displayed the number of chapters. Place the value in some suitable text, like 'The average number of chapters per day is '.
3. Where you displayed the number of chapters in the course, modify the output so it appears to two decimal places with the word chapters following the number created by the function. For example:

The average number of chapters per day is 3.33 chapters.

## Part 2 (Optional) Testing some of the other functions

If you have time, experiment with some of the additional functions that you have not used so far. Try to predict what the output will be before you view it.

# Chapter 4 Templates

## Aims

In this exercise, you will improve the modularity of your stylesheet by migrating some of your transformation code to new templates and adding other templates which will be called by name.

## Part 1 Adding a Copyright notice

1. You can either carry on working with your stylesheet from the previous exercise, or you can use the solution from the previous exercise. Either copy <LAB\_HOME>\labs\XPathFunctions\courseOutline.xslt  or <LAB\_HOME>\solutions\XPathFunctions\courseOutline.xslt into the <LAB\_HOME>\labs\Templates folder.
2. Add a new template with a name of copyright. There is no need for a match attribute here. In this new template, add a line that give displays a copyright notice in font size 1. This will look something like:

<font size='1'>(c) Conygre IT Limited 1999 - 2008</font>

1. After all other content inside the course template, add an <xsl:call-template> element with a call to the copyright template.
2. Put this call inside a <p> tag.
3. Test your stylesheet and confirm that the copyright notice appears

## Part 2 Migrating Content

1. Create a new template with the name courseBody. From within the template matching course, cut everything inside the <body> element and paste it into the new template
2. In its place, add an <xsl:call-template> element which calls this new template.
3. This now keeps various stylesheet sections separate from each other; the idea being that this makes your stylesheet cleaner and easier to maintain.
4. Test your stylesheet before continuing – the output should be exactly the same as before. This is because you have only modified the stylesheet layout – not the transformation

## Part 3 Passing Parameters

1. Locate the <xsl:call-template> element that you added in step 2 of part 2. Give it a closing tag instead of the shorthand closing and, inside the opening and closing tag, add an <xsl:with-param> element. This should pass a parameter called average containing the number of chapters divided by the number of days. This should look something like:

<xsl:call-template name='courseBody'>

<xsl:with-param name='average' select='count(contents/chapter) div duration'/>

</xsl:call-template>

1. Inside the courseBody template, add an <xsl:param> element to 'catch' this parameter. You do not need to supply a default value.
2. Locate the line that begins 'This means that one each day…' and find the <xsl:value-of> element on that line.
3. Delete all the content of the select attribute and replace it with $average.
4. This should result in the same output, but this time the average number of days was pre-calculated and passed down to the template using a parameter.
5. Test your stylesheet before continuing.

## Part 4 Using a global parameter value

1. Within courseOutline.xsl add an <xsl:param> element outside of the template. This will 'catch' the parameter that is passed into the stylesheet. Give the parameter a name of 'colour' and a default value of 'blue'.
2. Locate the font tag in your template and change its color value to '{$colour}'. This enables the stylesheet to make use of the parameter at this point.
3. Test your stylesheet and examine the results. If all has gone well, then you should see the chapter objectives displayed in blue. This is because no parameter has been passed in and therefore the default value has been used.

## Part 5 Passing the Parameter from XML Spy

1. You will now pass a parameter using XML Spy. In XML Spy, open the XML file to be transformed, that is <LAB\_HOME>\labs\Templates\buildingEffectiveXMLApplications.xml.
2. Click on the XSL menu, and select XSL Parameters.
3. Click inside the blue area just under the name section, and type the parameter name colour.
4. Click inside the blue area just under the XPath section, and enter the text &#39;green&#39;, making sure that you use quotes (if you do not it thinks green is an XPath expression referring to a node).
5. Finally, assign your <LAB\_HOME>\labs\AdvancedXSLT\courseOutline.xsl stylesheet to the XML document, and transform it using XML Spy. The objectives should now appear in the results tree in green.

## Part 6 Creating an XSLT Function

1. You will now create a function to calculate the average number of days that a course lasts for, and then you will call your function from a template. Ensure that your stylesheet is version 2.0 not 1.0.
2. Scroll to the end of the stylesheet and just before the closing <xsl:stylesheet> element add a <xsl:function> element. Give the function the name con:averageChapters, and give the con prefix a suitable namespace in the root stylesheet tag.
3. Specify the return type of the function as an xs:double. Set the xs prefix to be the XML Schema namespace http://www.w3.org/2001/XMLSchema.
4. Add two parameters to the function. One is the number of days, and one is the number of chapters. Set both parameters to be of type xs:integer.
5. Finally, in the body of the function, create a sequence with a select attribute that has the number of chapters divided by the number of days.
6. In the courseBody template, locate the value-of tag that displays the average number of chapters currently, and change it so that it now uses your function.
7. Check that it behaves as expected.

# Chapter 5 XSLT Flow Control

## Aims

In this exercise, you will add some of the flow control constructs to your stylesheet.

## Part 1 Working with the branching constructs

1. For this exercise you will need to use either the solution to the previous exercise, or your solution to the previous exercise.
2. Either copy <LAB\_HOME>\Labs\templates\courseOutline.xslt  or <LAB\_HOME>\Solutions\templates\courseOutline.xslt into the <LAB\_HOME>\labs\XSLTFlowControl folder.
3. Using XML Spy, open up <LAB\_HOME>\labs\XSLTFlowControl\courseOutline.xslt.
4. Add the functionality to display a list of only the chapter objectives that contain the text &#39;XML&#39; within them.
5. Modify the list of chapters so that the titles appear in alternate colours. Hint: You may wish to use the mod arithmetic operator for this. Use the if construct initially, and once you have that working, change it to use the choose/when construct.

## Part 2 Working with loops

1. You will now work with the for-each looping element. After the course outline is displayed, add the course objectives using a for-each loop. Display them in an unordered list.
2. You will now move your chapter template content into the course template by replacing the <xsl:apply-templates select='contents/chapter'/> with a for-each that renders the contents of your chapter template.
3. Now add a sort element that sorts the objectives alphabetically.

## Part 3 Putting it all together

Finally, in this part, you are to create a template that actually would result in a near production quality transformation. You may work in pairs on this exercise if you wish, as it is not as easy as it might first appear. Also, there is no solution provided for this part.

1. Tidy up the formatting of your current stylesheet to make it as neat as your HTML skills allow for!
2. Remove the list of objectives that begin with the text &#39;XML&#39;.
3. Modify the chapter list so that instead of being one large long list, it is in two columns running down the page of about equal length, with the chapters numbered appropriately. If you have Internet access, visit www.conygre.com/training/ and select an outline to get an idea of what is required. You will be recreating a basic version of the stylesheet that is used in the Web site. Don&#39;t worry about fonts and background colours, just get the layout to work. Note that it must work for courses with different numbers of chapters.

## Part 4 Working with for-each-group

You will now create a stylesheet that lists all the chapter objectives that contain the text XML, followed by all the chapter objectives that do not. You will do this using a for-each-group, where you will group the objectives based upon whether they contain XML in the text.

1. Create a new XSLT 2.0 Stylesheet document, and add a template matching on a course element.
2. Within the template, add a for-each-group element that selects the contents/chapter/objective elements and groups them by whether they contain the text XML (use the contains function).
3. Add a nested sort element to sort them by the current-grouping-key().
4. Add an unordered list, and loop around the current-group() outputting the value of the current node between <li></li> elements.
5. Save your file as courseOutlineGroups.xslt, and transform your XML document using the stylesheet and check that you have two lists of objectives. One contains all the objectives with XML in the text, and the other list contains the rest.
6. Finally, add headings to the two lists that say 'Here are the XML objectives' and 'Here are the non-XML objectives'. To do this, you will need to use an if element. Remember, the contains function used earlier returns a Boolean.
7. Transform your XML document again, and you should see two lists with the appropriate headings.

#

## Part 5 Optional Working with Regular Expressions

If you have time, and are comfortable with regular expressions, create a stylesheet that display all the chapter objectives that contain four letter acronyms.

#

# Chapter 6 XML Output

## Aims

In this exercise you will transform selected areas of XML into a different XML grammar.

## Part 1 Changing the Grammar

1. In this exercise you will _ **not** _ be continuing from where you left off in the previous exercise. In XML Spy, create a new XSL stylesheet and save it as <LAB\_HOME>\labs\XMLOutput\courses.xslt.
2. Within this file, create a new template which matches the root '/'.
3. Inside this template, add an XML element (plain XML _ **not** _ using <xsl:element>) called <Courses>.
4. Inside this element, use an <xsl:element> to define a new element called technicalCourse.
5. Inside this new element, use an <xsl:attribute> element to define a new attribute called title.
6. Within the <xsl:attribute>, use an <xsl:value-of> element with a select value of '/course/title'. You might want to consider using the normalize-space() function to remove the leading and trailing whitespace around the title.
7. After the title attribute define another attribute called duration and, again using <xsl:value-of> give it a value from '/course/duration'.
8. After the <xsl:value-of> element put a <xsl:text> element containing a space and the word days. This should look something like:

<xsl:attribute name='duration'>

<xsl:value-of select='/course/duration'/><xsl:text> days</xsl:text>

</xsl:attribute>

1. The final thing to put inside your new technicalCourse is a new <xsl:copy-of> with a select attribute of '/course/contents'. This should look something like:

<xsl:copy-of select='/course/contents'/>

1. Test your stylesheet against the buildingEffectiveXMLApplications.xml file in the same folder as your stylesheet before continuing.
2. Think about why you needed to use the <xsl:text> element. If you can&#39;t figure out why, simply remove it and re-run the stylesheet to get a clue.

## Part 2 Working with Namespaces

You will now modify the stylesheet so that it can cope with XML documents that also include a namespace, and in addition, will create an XML document that defines a namespace.

1. Open the file <LAB\_HOME>\labs\XMLOutput\buildingEffectiveXMLApplicationsNS.xml and review the content. Note that it is the same as the previous XML file except that it also incorporates a namespace.
2. Modify the stylesheet so that it incorporates a namespace declaration for the default namespace used in the buildingEffectiveXMLApplicationsNS.xml file, and use the prefix con. You will have a root element in your stylesheet element as shown below:

<xsl:stylesheet version='1.0' xmlns:xsl='http://www.w3.org/1999/XSL/Transform' **xmlns:con='www.conygre.com/v1/outline'** >

1. Declare a global variable to hold the new namespace value that is to be used in the result tree. The namespace value will be http://www.conygre.com/newnamespace, and the variable is to be called conygreNS. Remember to use extra quotes as it is a String!
2. Modify your element declarations so that the new element names now use the prefix c, and set the namespace for them to be the value of the conygreNS variable. For example:

<xsl:element name='c:Course' namespace='{$conygreNS}'>

1. Modify all references to elements in the source tree to have the prefix con. For example:

<xsl:value-of select=' **/con:course/con:duration**'/>

1. Finally, transform the buildingEffectiveXMLApplicationsNS.xml document using your stylesheet, and you will see a transformation result that is based upon the new namespace.

## Part 3 Creating Multiple Output Documents

In this exercise, you will create multiple output documents, one for each chapter in the course.

1. Create a new XSLT 2.0 Stylesheet and save it as multipleOutput.xslt.
2. Add a template matching on chapter, and within it, create a variable called filename to hold the following value:
generated/<chapter title>.xml.
 To create this, you will need to use the concat function.
3. Within the template, use the result-document element to create a file with the name set up in the variable (use an attribute value template { .. }), and then copy the entire chapter element into the output using the appropriate XSLT tag.
4. Transform the no namespace version of the course XML using the stylesheet, and you will see a set of new files created in the generated subfolder of the lab directory.

## Part 4 Optional Creating a Character Map

If you have time, add a character map to your stylesheet. You could try swapping all the X characters for V characters. See if VML looks better in the output than XML!

#

#

# Chapter 7 Combining Stylesheets

## Aims

In this exercise you will import one stylesheet into another and override one of the imported templates.

## Part 1 Importing the stylesheet

1. In XML Spy, open up <LAB\_HOME>\labs\CombiningStylesheets\importedOutline.xsl and examine the contents. You will notice that it is the same or very similar to the stylesheet you have been creating. This is the stylesheet that you will import into another stylesheet.
2. Create a new stylesheet in XML Spy and save it as <LAB\_HOME>\labs\CombiningStylesheets\courseOutline.xsl.
3. Add an <xsl:import> element and point it to the importedOutline.xsl file.
4. Run this new stylesheet and you should find that it works exactly as other stylesheets before; even though it contains only one line. This is because the processor is running all the imported templates; which results in exactly the same output as on previous runs with your other stylesheets.

## Part 2 Overriding a template

1. In courseOutline.xsl add a new template which matches objective. This will override the same template in the imported stylesheet.
2. Inside this template, use a font tag to specify that the font colour should be red.
3. Within this font tag, add a <xsl:value-of select='.'/> element.
4. Run the stylesheet again and notice the difference in the display of the objective elements. This is because the processor is using the new template in preference over the imported one.
5. There are far too many objectives displayed here, and the previous template had a test to specify which objectives were to be displayed. Replace the <xsl:value-of> that you created in the last step with a <xsl:apply-imports/> element.
6. This should now call the imported template; but still display the output in red. The processor is now using both the new template and the imported one.
7. Test your stylesheet.


