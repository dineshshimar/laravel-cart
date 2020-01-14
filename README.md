# laravel-cart
Laravel Package for the management of cart.

Install the Package by :
composer require devbuddy/cart

After successfully installation configure the package into your project.

Add where need to use the Cart : 
```php
use Cart;
```

# Laravel 5 & 6 Shopping Cart

A Shopping Cart Implementation for Laravel Framework

## INSTALLATION

Install the package through [Composer](http://getcomposer.org/).

For Laravel 5.1~:
`composer require "devbuddy/cart"`


## CONFIGURATION

1. Open config/app.php and add this line to your Service Providers Array.
   NOTE: If you are using laravel 5.5 or above, this will be automatically added by its auto discovery.


## Quick Usage Example

```php
// Quick Usage with the Product Model Association & User session binding

$Product = Product::find($productId); // assuming you have a Product model with id, name, description & price

// add the product to cart
$rowid = Cart::insert(array(
    'id' => $Product->id,
    'name' => $Product->name,
    'price' => $Product->price,
    'quantity' => 4,
    'options' => array()
));

// update the item on cart
Cart::update($rowid,[
	'quantity' => 2,
	'price' => 98.67
]);

// delete an item on cart
Cart::remove($rowid);

// view the cart items
$items = Cart::contents();
foreach($items as $row) {

	echo $row['id']; // row ID
	echo $row['name'];
	echo $row['qty'];
	echo $row['price'];
	
}

// FOR FULL USAGE, SEE BELOW..
```

##What is a Row ID?
The row ID is a unique identifier that is generated by the cart code when an item is added to the cart. The reason a unique ID is created is so that identical products with different options can be managed by the cart.

For example, let’s say someone buys two identical t-shirts (same product ID), but in different sizes. The product ID (and other attributes) will be identical for both sizes because it’s the same shirt. The only difference will be the size. The cart must therefore have a means of identifying this difference so that the two sizes of shirts can be managed independently. It does so by creating a unique “row ID” based on the product ID and any options associated with it.


### METHODS!


```php
Cart::insert();
Cart::update();
Cart::total();
Cart::remove();
Cart::total_items();
Cart::contents();
Cart::get_item();
Cart::has_options();
Cart::product_options();
Cart::format_number();
Cart::destroy();
```

See More Examples below:

Adding Item on Cart: **Cart::insert()**

There are several ways you can add items on your cart, see below:

```php

// Simplest form to add item on your cart
Cart::add(455, 'Sample Item', 100.99, 2, array());

// array format
Cart::insert(array(
    'id' => 456, // inique row ID
    'name' => 'Sample Item',
    'price' => 67.99,
    'quantity' => 4,
    'options' => array()
));

// add multiple items at one time
Cart::insert(array(
  array(
      'id' => 456,
      'name' => 'Sample Item 1',
      'price' => 67.99,
      'quantity' => 4,
      'options' => array()
  ),
  array(
      'id' => 568,
      'name' => 'Sample Item 2',
      'price' => 69.25,
      'quantity' => 4,
      'options' => array(
        'size' => 'L',
        'color' => 'blue'
      )
  ),
));
// NOTE:
// Please keep in mind that when adding an item on cart, the "id" should be unique as it serves as
// row identifier as well. If you provide same ID, it will assume the operation will be an update to its quantity
// to avoid cart item duplicates
```

Updating an item on a cart: **Cart::update()**

Updating an item on a cart is very simple:

```php
$data = array(
        'rowid' => 'b99ccdf16028f015540f341130b6d8ec',
        'qty'   => 3
);

Cart::update($data);

// Or a multi-dimensional array

$data = array(
        array(
                'rowid'   => 'b99ccdf16028f015540f341130b6d8ec',
                'qty'     => 3
        ),
        array(
                'rowid'   => 'xw82g9q3r495893iajdh473990rikw23',
                'qty'     => 4
        ),
        array(
                'rowid'   => 'fh4kdkkkaoe30njgoe92rkdkkobec333',
                'qty'     => 2
        )
);

Cart::update($data);
//You may also update any property you have previously defined when inserting the item such as options, price or other custom fields.
$data = array(
        'rowid'  => 'b99ccdf16028f015540f341130b6d8ec',
        'qty'    => 1,
        'price'  => 49.95,
        'coupon' => NULL
);

$this->cart->update($data);
```

Removing an item on a cart: **Cart::remove()**

Removing an item on a cart is very easy:

```php
/**
 * removes an item on cart by item ID
 *
 * @param $rowid
 */

Cart::remove($rowid);

```

Getting an item on a cart: **Cart::contents()**

```php

Cart::contents();
```

Still feeling confuse on how to do custom database storage? Or maybe doing multiple cart instances?
Contact me via git.


## License

The Laravel Shopping Cart is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT)

### Disclaimer

THIS SOFTWARE IS PROVIDED "AS IS" AND ANY EXPRESSED OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE AUTHOR, OR ANY OF THE CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
