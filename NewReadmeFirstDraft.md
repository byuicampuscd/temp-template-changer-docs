# Template Changer

Used to change a group of html files to follow a template.

## To know or do beforehand

- The structure of course html pages and supporting files
- Node
- Github
- [Handlebars](http://handlebarsjs.com/) (at least expressions and that looks like html - here or discuss in template?)

## Setup

Install the template changer by running the following in the command line:<br>
npm install –g "https://github.com/byuicampuscd/template-changer"

Run "template-changer" to see how it can be used

## Steps to follow

- Download all the files
- Make your template by looking at what you've got and what you want it to be
- Run it
- Once run, go and check that to make sure that all of those files successfully went through
- If it didn't, a folder is made that you can go look at to find the issue(s)
- Then add the needed logic
- Repeat until all are done, and is one folder (not any subfolders of errors)

## Making the template

For each template you make, you will need to actually create two files. One is a simple text file declaring the variables to use in the template. The other is a .handlebars file that contains the actual template. If you don't know at least the basics of handlebars, please go to the link given above before continuing.

### Variables

Run "template-changer -v" to see an example of the variables file.

You will notice three columns. They are: Variable Name | Element Selector | Type of Variable

These variables act like any other variable in programming, and you can name them as you like. This must match what will go into the handlebars expression. The only restrictions are given by Handlebars here: (http://handlebarsjs.com/expressions.html#basic-blocks).

The element selector works exactly the same as what you're used to from CSS.

The type of variables defines what information you want to extract from the element. The different types to choose from are as follows:
- html - This will extract the innerHtml of the element
- text - This will only extract the text inside the element (ignoring tags, etc.)
- outerhtml - This will extract everything html extracts, but includings the surrounding tag
- bool - This will be set to true if the element exists, and false if it does not.
- ... - Any other value will be assumed to be an attribute, in which case its value is extracted

You probably also noticed an 'array' after a variable type. This is an optional parameter which if used must follow the variable type with a pipe ( | ) in between, and indicates that the variable is an array. Thus, given the selector p and type html and array, it becomes an array holding the inner html of each p element in the file.

The asterisks before the variable names indicates that those variables are mandatory and thus forces an error if the element is not found. What follows when this happens will be explained later.

To create this file yourself, just create a new .txt file in the folder containing the html files to change, and fill it in following the format of the example. (Note that the spacing between bars was for stylistic purposes, and is not necessary to function correctly; also note that the ordering of the list of variables does not matter)

As a last note here, there are two built-in variables - fileName and fileContents - as the HELP section indicated when you run template-changer without parameters. The fileName variable gives you the name of the file, including the extension. The fileContents gives you everything in the html file. This is mostly helpful if you come across something like a file that only contains the 'guts' without the beginning and ending parts of a normal html page. You could then just use the variable to include it all in the new file between those missing parts you would then create.

### Template

Run "template-changer -t" to see an example of the template file.

Before reading this, you should have a general idea of how a handlebars template works. The template-changer attempts to create a new version of each html file using the template file you create. When it runs into a variable in a handlebars expression, it will try to use the specified information you defined in the variables file which it obtains from the old version of the html file. 

For example, if in the template file you create the title like this in the template: `<title>{{title}}</title>` and have this in the variables file: `title | title | text` , and the old html file has this: `<title>Example Title</title>` , then the program will create a new html file with this: `<title>Example Title</title>` .

Another example is using boolean logic, where if you created a boolean (bool) variable called isSplash which is set to true if the old html file contains the class="splash" attribute (using the selector .splash), then you can use the following code to define html to include if that element was found and another set of html to include if not:

```html
    {{#if isSplash}}
    <div id="header" class="splash">
        Some Html...
    </div>
    {{else}}
    <div id="header">
        Possibly different html...
    </div>
    {{/if}}
```

Note that the template file should be a .handlebars file.

## Running template-changer

Now you should have a copy of the html files downloaded to a new folder and your template made and placed in the same folder. Once that is done, in the command line go to the folder containing the files, and run the template-changer with the variable and template files as parameters, respectively. This will create a new folder with the modified html files. Open the folder, and verify the files are all there. 

If a subfolder appears, it means the program had an error trying to change the files contained inside. This is what happens when an element wasn't found for a variable you indicated as mandatory with an asterisk. Note that the subfolder name indicates what variable(s) had the error. Now you can go in to the files, see what caused the issue and what you do need, and correct/add to your variables or template to fix the issue. Once you do this, make sure you're in the folder with the html files in the command line and run the program again. Notice that this creates a new folder with the same name, except the number increments by 1. This allows you to repeat this process, while keeping a copy of every step.

Once you have a folder with all the modified files and no subfolders containing problem files, you've finished the modifications. Now you just need to upload the new html files to replace the old ones.

## Example?

## Misc

- Bookmarklet