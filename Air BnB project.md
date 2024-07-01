

### Basic project structure, timeline and taskpool



| Date Range            | Team Member | Task Description                                                             | Key Deliverables                                                                   |
| --------------------- | ----------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| **May 29 - June 1**   | `Yaroslav`  | Set up Rails environment, configure database, and initialize CI/CD pipeline. | Rails environment ready, database connected, CI/CD operational.                    |
| **June 1 - June 3**   | `Dimitris`  | Implement user authentication with Devise, including roles (guest, host).    | Authentication system live, roles defined and functioning.                         |
| **June 2 - June 4**   | `Jurij`     | Create basic HTML/CSS structure for Home page and integrate Bootstrap.       | Home page structured and styled.                                                   |
| **June 2 - June 4**   | `Yaroslav`  | Develop frontend skeleton for overall application layout.                    | Consistent navigation, header, and footer across the site.                         |
| **June 5 - June 7**   | `Vaida`     | Build CRUD operations for property management, set up Active Storage.        | Property models created, CRUD functionality operational.                           |
| **June 5 - June 7**   | `Jurij`     | Design and implement Login/Registration pages using HTML/CSS.                | User-friendly login and registration pages functional.                             |
| **June 6 - June 8**   | `Yaroslav`  | Implement search functionality with filters and a booking system.            | Search and booking features functional, integrated with backend.                   |
| **June 9 - June 10**  | `Jurij`     | Enhance property listing page with interactive maps and dynamic updates.     | Property listings interactive, map and dynamic content working.                    |
| **June 11 - June 12** | `All`       | Final integration of frontend and backend, adjust responsive design.         | Seamless interaction between frontend and backend, site responsive on all devices. |
| **June 12**           | `Yaroslav`  | Oversee final deployment to Heroku, perform basic load testing.              | Application deployed, basic performance validated.                                 |






To create Ruby on Rails routes for the provided schema, you will typically use the `config/routes.rb` file in your Rails application. Here are the suggested routes based on your schema, including nested routes where appropriate:

### Suggested Routes

```ruby
Rails.application.routes.draw do
  # Users routes
  resources :users, only: [:index, :show, :create, :update, :destroy] do
    resources :orders, only: [:index, :show, :create, :update, :destroy]
  end

  # Orders routes
  resources :orders, only: [:index, :show, :create, :update, :destroy]

  # Gears routes
  resources :gears, only: [:index, :show, :create, :update, :destroy]
end
```

### Explanation

1. **Users Routes**:
   - **index**: Lists all users.
   - **show**: Displays a specific user.
   - **create**: Creates a new user.
   - **update**: Updates a specific user.
   - **destroy**: Deletes a specific user.

2. **Nested Orders Routes**:
   - Nested under users to list all orders for a specific user.
   - **index**: Lists all orders for a specific user.
   - **show**: Displays a specific order for a specific user.
   - **create**: Creates a new order for a specific user.
   - **update**: Updates a specific order for a specific user.
   - **destroy**: Deletes a specific order for a specific user.

3. **Standalone Orders Routes**:
   - **index**: Lists all orders.
   - **show**: Displays a specific order.
   - **create**: Creates a new order.
   - **update**: Updates a specific order.
   - **destroy**: Deletes a specific order.

4. **Gears Routes**:
   - **index**: Lists all gears.
   - **show**: Displays a specific gear.
   - **create**: Creates a new gear.
   - **update**: Updates a specific gear.
   - **destroy**: Deletes a specific gear.

### Example of Generated Routes

To see the generated routes, you can run `rails routes` in your terminal. Here is an example of what the routes might look like:

```
users       GET    /users(.:format)                        users#index
            POST   /users(.:format)                        users#create
 user       GET    /users/:id(.:format)                    users#show
            PATCH  /users/:id(.:format)                    users#update
            PUT    /users/:id(.:format)                    users#update
            DELETE /users/:id(.:format)                    users#destroy

 user_orders GET    /users/:user_id/orders(.:format)       orders#index
             POST   /users/:user_id/orders(.:format)       orders#create
  user_order GET    /users/:user_id/orders/:id(.:format)   orders#show
             PATCH  /users/:user_id/orders/:id(.:format)   orders#update
             PUT    /users/:user_id/orders/:id(.:format)   orders#update
             DELETE /users/:user_id/orders/:id(.:format)   orders#destroy

 orders      GET    /orders(.:format)                      orders#index
             POST   /orders(.:format)                      orders#create
  order      GET    /orders/:id(.:format)                  orders#show
             PATCH  /orders/:id(.:format)                  orders#update
             PUT    /orders/:id(.:format)                  orders#update
             DELETE /orders/:id(.:format)                  orders#destroy

 gears       GET    /gears(.:format)                       gears#index
             POST   /gears(.:format)                       gears#create
  gear       GET    /gears/:id(.:format)                   gears#show
             PATCH  /gears/:id(.:format)                   gears#update
             PUT    /gears/:id(.:format)                   gears#update
             DELETE /gears/:id(.:format)                   gears#destroy
```

These routes will allow you to manage users, orders, and gears effectively within your Rails application.

