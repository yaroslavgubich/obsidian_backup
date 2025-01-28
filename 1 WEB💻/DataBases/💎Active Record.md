How to #connect tables with #foreign #key

![[Pasted image 20240319161157.png]]

#activerecord #convention #syntax
Your model class name should be in `UpperCamelCase`, singular form (e.g. `SportsCar`).

Your table name should be in `lower_snake_case`, plural form (e.g. `sports_cars`).

#ActiveRecord’s magical 1:1 mapping between records of your DB and instances of your models relies entirely on this convention!
Active Record is a powerful ORM (Object-Relational Mapping) tool used in web development, particularly with Ruby on Rails, for interacting with databases in an object-oriented manner. Below is a cheat sheet of common Active Record commands that can help you manage your database more efficiently. This list is not exhaustive but covers many of the essential commands you'll find useful on a day-to-day basis.

### Creating Records

- **New + Save**
  ```ruby
  user = User.new(name: "Yaroslav", email: "yaroslav@example.com")
  user.save
  ```
  Creates a new instance and then saves it to the database.

- #Create**
  ```ruby
  user = User.create(name: "Yaroslav", email: "yaroslav@example.com")
  ```
  Instantiates a new instance and saves it to the database in one step.

### Reading Records

- #Find**
  ```ruby
  user = User.find(1)
  ```
  Finds a record by its ID.

- #Find_by**
  ```ruby
  user = User.find_by(name: "Yaroslav")
  ```
  Finds the first record matching the specified conditions.

- #Where**
  ```ruby
  users = User.where(name: "Yaroslav")
  ```
  Returns an ActiveRecord::Relation object containing all records matching the conditions.

### Updating Records

- #Update Attribute**
  ```ruby
  user.update_attribute(:email, "newemail@example.com")
  ```
  Updates a single attribute, bypassing validations.

- **Update**
  ```ruby
  user.update(name: "New Name", email: "newemail@example.com")
  ```
  Updates multiple attributes at once, performing validations.

- #Update_all**
  ```ruby
  User.where(name: "Yaroslav").update_all(activated: true)
  ```
  Updates all records matching conditions without instantiating them.

### #Deleting Records

- #Destroy**
  ```ruby
  user = User.find(1)
  user.destroy
  ```
  Deletes a record from the database.

- #Destroy_all**
  ```ruby
  User.where(name: "Yaroslav").destroy_all
  ```
  Deletes all records matching conditions from the database.

### Associations

- **Belongs_to / Has_many / Has_one / Has_many :through**
  Define relationships between different models.

### #Validations

- **Validates**
  ```ruby
  validates :name, presence: true
  ```
  Ensures the presence of a name attribute before saving the record.

### Migrations

- #Create_table**
  ```ruby
  create_table :users do |t|
    t.string :name
    t.string :email

    t.timestamps
  end
  ```
  Creates a new table in the database.

- #Add_column**
  ```ruby
  add_column :users, :admin, :boolean, default: false
  ```
  Adds a new column to an existing table.

- #Rename_column**
  ```ruby
  rename_column :users, :name, :username
  ```
  Renames a column in a table.

### Conclusion

This cheat sheet provides a solid foundation for performing CRUD operations, managing associations, ensuring validations, and handling migrations with Active Record. As you become more familiar with these commands, you'll discover more advanced features and techniques that Active Record offers, such as scopes and callbacks. Remember, Active Record is a vast library, and the Rails Guides are an excellent resource for deeper exploration.
Building on the foundational #commands provided earlier, let's explore more #ActiveRecord commands that offer extended functionality and help manage your database and models in a Ruby on Rails application. These commands will touch on scopes, more complex queries, callbacks, and some additional utilities that can enhance your productivity.

### Scopes

- #Scope**
  ```ruby
  scope :active, -> { where(active: true) }
  ```
  Defines a scope for reusing common queries. You can use it like `User.active` to get all active users.

### Complex Queries

- #Select**
  ```ruby
  User.select(:name, :email)
  ```
  Specifies the fields to be selected from the database.

- #Order**
  ```ruby
  User.order(:name)
  ```
  Orders the result set based on the specified column.

- #Limit**
  ```ruby
  User.limit(5)
  ```
  Limits the number of records returned from the query.

- #Offset**
  ```ruby
  User.offset(10).limit(5)
  ```
  Skips the first 10 records, useful for pagination.

- #Group**
  ```ruby
  User.group(:status).count
  ```
  Groups the records by the specified column and performs a count per group.

- **Having**
  ```ruby
  User.group(:status).having("count(status) > 2").count
  ```
  Allows to specify conditions on the `GROUP BY` fields.

### Callbacks

- #Before_save**
  ```ruby
  before_save :normalize_name
  def normalize_name
    self.name = name.downcase.titleize
  end
  ```
  Executes the specified method before saving an object.

- #After_create**
  ```ruby
  after_create :send_welcome_email
  def send_welcome_email
    UserMailer.welcome_email(self).deliver_later
  end
  ```
  Executes after a new object is created.

### Transactions

- #Transaction**
  ```ruby
  ActiveRecord::Base.transaction do
    user1.save!
    user2.save!
  end
  ```
  Ensures that the block of operations is executed within a database transaction. If an exception is raised, all database changes within the transaction are rolled back.

### Polymorphic Associations

- #Polymorphic Association**
  ```ruby
  class Picture < ApplicationRecord
    belongs_to :imageable, polymorphic: true
  end

  class Employee < ApplicationRecord
    has_many :pictures, as: :imageable
  end

  class Product < ApplicationRecord
    has_many :pictures, as: :imageable
  end
  ```
  Allows a model to belong to more than one other model, on a single association.

### Counter Cache

- #Counter #Cache**
  ```ruby
  class Comment < ApplicationRecord
    belongs_to :post, counter_cache: true
  end
  ```
  Keeps a cache count of the number of associated objects on the associated model for efficiency.

### Conclusion

Active Record offers a rich set of utilities to make database interactions more efficient, expressive, and convenient. The commands and features explored here are just the tip of the iceberg. As you delve deeper into Active Record, you'll find even more advanced features such as eager loading, connection pooling, and more. The official Rails Guides and API documentation are excellent resources to learn these advanced topics and stay updated with new features and best practices.
In the context of a Ruby on Rails migration, `add_reference` adds a reference (i.e., a foreign key) to another table, indicating a relationship between two models. This is part of ActiveRecord's migration API, which provides a way to alter the database schema in a structured and reversible manner. Adding a reference is commonly used to establish associations between models, such as a `belongs_to` relationship.

When you use #add_reference in a migration, Rails will automatically add a foreign key column to the table you specify, along with an index on this column for performance reasons. The foreign key typically points to the `id` column of the associated table, which is the primary key.

### Example of `add_reference`

Suppose you have a `patients` table and you want to establish a `belongs_to` relationship with an `interns` table, meaning each patient is associated with an intern. You would use `add_reference` in a migration like so:

```ruby
class AddInternIdToPatients < ActiveRecord::Migration[6.0]
  def change
    add_reference :patients, :intern, foreign_key: true
  end
end
```

Here’s what happens with this migration:

- **`:patients`**: This specifies the table you're modifying, in this case, the `patients` table.
- **`:intern`**: This is the name of the reference you're adding. Rails will append `_id` to this symbol to create the column name `intern_id` in the `patients` table. This will be the foreign key column.
- **`foreign_key: true`**: This option tells Rails to enforce a foreign key constraint at the database level, ensuring referential integrity. This means the database will prevent you from adding a patient with an `intern_id` that doesn't exist in the `interns` table.

### Benefits of `add_reference`

- **Simplicity**: It abstracts away the complexities of SQL, providing a simple, Ruby-esque way to modify database schemas.
- **Safety**: By automatically creating an index, it ensures that queries filtering or joining on the foreign key are efficient.
- **Integrity**: The `foreign_key: true` option enforces database referential integrity, preventing orphaned records.

Using `add_reference` is a best practice for defining relationships in a Rails application, making it easier to maintain and understand the database schema.****
#ActiveRecord #cheatsheet #documentation 

https://guides.rubyonrails.org/active_record_migrations.html#using-the-change-method