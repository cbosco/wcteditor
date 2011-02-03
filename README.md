# WCTeditor #

A super-simple text editor for modern browsers. Supports:

+ bold
+ italic
+ underline
+ numbered lists
+ bulleted lists
+ links
+ stripping html (except line breaks/paragraphs)
+ spell-check via callback (_coming soon!_)

Tested so far and works ok in:

+ FF 3.6
+ Chrome 8
+ Safari 5
+ Opera 11
+ IE 7+
+ __NOT__ mobile WebKit

## Usage ##

Requires jQuery and the jQuery templates plugin (there's also a [version with no template dependency](https://github.com/cbosco/wcteditor/)). Get those and then apply the WCTeditor plugin to a textarea with some options:

	$("#myTextArea").WCTeditor({
		showNumList: true,
		showBullList: true,
		pathToPlugin:"../"
	});

Yay! Done.

## Options ##

### showBold ###
boolean:
Whether or not you'd like the bold button to be shown. On by default.

### showItalic ###
boolean:
Whether or not you'd like the italicize button to be shown. On by default.

### showUnderline ###
boolean:
Whether or not you'd like the underline button to be shown.

### showNumList ###
boolean:
Whether or not you'd like the ordered list button to be shown.

### showBullList ###
boolean:
Whether or not you'd like the unordered list button to be shown.

### showLink ###
boolean:
Whether or not you'd like the link button to be shown. On by default.

### showStripHtml ###
boolean:
Whether or not you'd like the strip/clean up HTML button to be shown.

### showSpellCheck ###
boolean:
Whether or not you'd like the spellcheck button to be shown.

### userClasses ###
array of strings:
CSS class(es) you'd like to have applied to the div that wraps the editor.

### defaultText ###
string:
Text you want the editor to display with, if different than what's in your textarea.

### showCharCount ###
boolean:
Whether or not you'd like to show a character counter. See below for where to change the way the character counter works.

### charCountTmpl ###
string:
The template for your character counter. This can be just text or some HTML, but you need to insert "{{html chars}}" where you want the count to actually appear.

### maxLength ###
integer:
The maximum length of the user's input, including HTML, if different than the maxlength of your textarea.

### spellcheckUrl ###
string:
Path to the spellchecking service you'd like to call. 

### pathToPlugin ###
string:
Location of this plugin (i.e., location of WCTeditor.js) relative to the file it's being implemented in.

### theme ###
string:
A directory name. The plugin will look for a stylesheet at [pathToPlugin]/themes/[theme]/WCTeditor.css

### placeholderText ###
string:
Helpful text that will display within the editor while it is empty, if defaultText is not set and the textarea is empty.

## Functions ##

You may want to override some of these to change the default functionality.

### applyFormatting ###
Applies the basic designMode commands.

### updateTextarea ###
Pushes changes to the editor to your textarea, then calls updateCharCount if it's enabled.

### updateCharCount ###
Updates the character count. Counts down from your specified maximum, then goes to negative. Assigns the CSS class "tooLong" to the count only once it goes negative.

### updateButtons ###
Updates the state of the formatting buttons depending on the cursor location.

### setLink ###
args: leftPosition (left position of formatting button)

Displays the interface to set a URL and wires up the button in that interface to update the editor markup.

### stripHTML ###
Removes all markup except paragraphs and line breaks.

### stripHTMLComments ###
Removes HTML comments from content pasted into the editor.

### spellcheck ###
IE-only implementation, because other browsers include spellcheck. Sends the text within the editor to the service specified by the spellcheckUrl property, and expects an array of results in the format:

	{originalWord: string, suggestions: []}

Wraps each misspelling in a font tag, and wires up an event handler to display a small window with the suggestions and an option to ignore the misspelling. Clicking a suggestion replaces the misspelling and remove the font tag, clicking ignore simply removes the font tag.
