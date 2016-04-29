define - does this create the js "class object" or DOM anywhere in memory?
alias - alias name for adding this component to another component
if u have an alias - why do u need an id? you must be able to refer to the object using the alias itself - to get a handle of the object to call events of the object or to set data in the object
what is the need to have an initComponent method when u have the constructor where in you can do all the initialization	
shouldn' the controller pass a store reference to the view? - why should you always register the required store for each view?
if you want a particular cell to be rendered in a particular way - say for example you want a particualr cell to be displayed as a download hyperlink? - do u have another object for it or do u have a template for it
if you are getting the values from the parent container, how do u do it?
if you are manipulating the DOM state of the parent container - how do u do it - through Ext.getCmp()?
if you are manipulating the DOM state of the child container - how do you do it?
why don't we use Ext.create over xtype?
Is extjs strongly typed - in the sense can you assign to an incompatible type, if yes how does extjs handle this?
will it be random behavior or a runtime error or compatibility check error when the corresponding page load is attempted?


session 2:
lazy initialization - rendering or putting the object in the DOM and displaying the new DOM if and only if that particular component is invoked
instantiation - is rendering the object or putting the object in the DOM tree
configuration - is creating the object, and having the DOM structure somewhere in memory?

xtype - some components will not be instantiated until they are called, for example clicking on a particular tab;
so xtype ensures that the component is configured (corresoponding DOM is somwhere in memory)and whenever it is called - it is instantiated / rendered (DOM is put into the appropriate place in the document)

lazy initialization and concurrency have some relationships


xtype vs Ext.create
http://skirtlesden.com/articles/config-objects-on-the-prototype

CONCEPT : if you put in references in the protoype - a reference is a non primitive, can be a function, can be a date, can be another component, the reference type is common across all the objects which is is an issue

Ext.define('MyPanel', { 
    extend: 'Ext.panel.Panel', 
 
    items: [ 
        Ext.create('Ext.button.Button', {text: 'Button'}) 
    ] 
});

Ext.create('MyPanel', {height: 100, width: 100}); 
Ext.create('MyPanel', {height: 100, width: 100});
this creates only one button in the 2nd panle, the 1st panel does not have the button, i.e it results in a sahred instance of the button
can be rectified by using the xtype, which just configures the button, however the instantiation is lazy

Ext.define('ExtensiblePanel', { 
    extend: 'Ext.panel.Panel', 
 
    initComponent: function() { 
        this.items = this.createItems(); 
        this.callParent(); 
    }, 
 
    createItems: function() { 
        return [ 
            {text: 'Button', xtype: 'button'} 
        ] 
    } 
});


""mutating and sharing""

there is a difference between rendering(when: initial, who: component, what: creating the DOM element) and layout (layout is just the positining and size)
---------------------------------------------------------------

2 ways to create a global scoped object
this.foo
var foo;



