How to create testing DB ?
#active #record
#create #DB
![[Pasted image 20240314100830.png]]

![[Pasted image 20240314100839.png]]
#test #DB 
![[Pasted image 20240314100922.png]]
#delete #drop #db with all lines and shell 
#create #file with #timestemp #date and #time
``` ruby
TIMESTAMP=`rake db:timestamp`
touch db/migrate/${TIMESTAMP}_create_restaurants.rb
```
#migration #class  #create


```ruby
class CreateRestaurants < ActiveRecord::Migration[7.0]
  def change
    create_table :restaurants do |t|
      t.string :name
      t.string :address
      t.timestamps # adds 2 columns, `created_at` and `updated_at`
    end
  end
end
```
how to #update #db #table #add ? If client wants "RATING" for ex.
1 Step: update your blueprint 


![[Pasted image 20240314131532.png]]
2 Step: #update #timestamp and file 

``` ruby
TIMESTAMP=`rake db:timestamp`
touch db/migrate/${TIMESTAMP}_add_rating_to_restaurants.rb
```

3 Step: 

``` ruby
# db/migrate/********_add_rating_to_restaurants.rb
class AddRatingToRestaurants < ActiveRecord::Migration[7.0]
  def change
    add_column :restaurants, :rating, :integer, default: 0, null: false
  end
end
```

![[Pasted image 20240316114844.png]] #add #data to a #table with #migrations 

#populate #db with #fake #data 
use ruby faker 
https://www.rubydoc.info/github/faker-ruby/faker

use #app #console 

``` css
rake console 

```
what is #erb shortly ?

ERB stands for "Embedded Ruby" and is a templating system that embeds Ruby code within a text document. It's often used in Ruby on Rails applications to create dynamic web pages. ERB allows you to place Ruby code within special tags in an HTML file, which the ERB templating engine then evaluates and replaces with actual Ruby code output when the page is requested. This enables the creation of web pages with content that can change depending on the state of the application, user data, or other factors.

ERB syntax involves two main types of tags:

1. `<% %>`: This tag encloses Ruby code that is executed but not printed to the output.
2. `<%= %>`: This tag encloses Ruby code whose result is printed into the HTML document at that location.

For example, you can use ERB to iterate over an array of items and display each item within an HTML list:

``` ruby
<ul>
  <% @items.each do |item| %>
    <li><%= item %></li>
  <% end %>
</ul>
```

In this code:

- The `<% %>` tag runs Ruby code (`@items.each`) without producing output itself.
- The `<%= %>` tag outputs the value of `item` into the HTML.

**Conclusion:**

ERB is a flexible and powerful tool for Ruby on Rails developers, allowing for the dynamic generation of web content by embedding Ruby code within HTML templates. This facilitates creating responsive and interactive user interfaces that can display content based on the application's state or user interactions.

How to do #get #post or #patch with #ruby ?
![[Pasted image 20240316152438.png]]

