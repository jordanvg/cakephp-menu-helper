cakephp-menu-helper
===================

Simple helper for [CakePHP](http://cakephp.org) that detects if a link routes to the current controller and styles a list element accordingly.

Based off of [MenuHelper by Malte Wassermann](http://www.maltewassermann.com/blog/2009/09/24/Menu_highlighting_with_CakePHP_What_s_the_active_item), but all I was using it for was to highlight menu items from the current controller so I figured I could do away with the regex and have the highlighting based off of the link's routes.

## Features
* wraps all passed links with list ```<li>``` elements
* detects if the passed link routes to the current controller, then applies a specified style to the list element
* new: support third param to set extact link mathching or not. It's usefull for catching all controller link ( add, view, edit, etc.. ) 
## Installation

### CakePHP >= 2.2
Install to ```app/View/Helper/```.

__For CakePHP 2.x before 2.2:__ you must replace [```Hash::merge()```](http://book.cakephp.org/2.0/en/core-utility-libraries/hash.html) with [```Set::merge()```](http://api20.cakephp.org/class/set#method-Setmerge).

## Usage
After installing you must include ```'Menu'``` in the ```$helper``` array of any controllers you want to use it in. To have it available to all controllers, include ```'Menu'``` in the ```$helper``` array in ```app/Controller/AppController.php```.

In your controller:
```php
// app/Controller/ExampleController.php
class ExampleController extends Controller {
public $helpers = array( ... , 'Menu')
...
}
```

In your view:
```php
// app/View/Example/view.ctp
...
<ul>
  <?php echo $this->Menu->item($this->Html->link('Home', '/home')); ?>
  <?php echo $this->Menu->item($this->Html->link('Example', '/example/add')); ?>
  <?php echo $this->Menu->item($this->Html->link('Example', array('controller' => 'example', 'action' => 'index')); ?>
  <?php echo $this->Menu->item($this->Html->link('Example', '/examplealternate')); ?>
  <?php echo $this->Menu->item($this->Html->link('About', '/about'), array('class' => 'specialClass')); ?>
  <?php echo $this->Menu->item($this->Html->link('Contact', array('controller' => 'contact', 'action' => 'index')); ?>
</ul>
...
```
Assume you were navigated to ```http://yourapp/example/view```, which is an action of your ```ExampleController```. When the above code is executed the following would happen:
* all the links would be of the form ```<li><a href="..."></a></li>```, and any attributes passed for the ```<li>``` elements will be preserved
* the links that route to ```ExampleController``` in ```app/Config/routes.php``` will have the specified class attached to the ```<li>``` element to signify the controller is currently active
* links can be passed in string form, or array form, and will be properly detected as the current controller as long as the route is known by Cake
* i.e. ```/examplealternate``` would also have the class attached to it assuming it was set to route to ```ExampleController``` in ```routes.php```


## TODO
* I know how useful it would be to only apply the style to a link that routes to the controller _and_ action
* properly convert Malte's original regex version of MenuHelper to CakePHP 2.0

## License

This code is licensed under the [MIT license](http://www.opensource.org/licenses/mit-license.php).
