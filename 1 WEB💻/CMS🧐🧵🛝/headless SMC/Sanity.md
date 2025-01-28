

#bash #script to #generate #query #fileStructure 

WARNING ⚠️⚠️⚠️⬇️ CHANGE ROOT FOLDER 
#!/bin/bash

# Define the base folder

BASE_DIR="./sanity_barcoblanco"

# Create the queries directory if it doesn't exist
mkdir -p "$BASE_DIR/queries"

# Create the files
touch "$BASE_DIR/queries/productQueries.ts"
touch "$BASE_DIR/queries/bannerQueries.ts"
touch "$BASE_DIR/queries/index.ts"

# Add template code to each file
echo "// Queries related to products" > "$BASE_DIR/queries/productQueries.ts"
echo "// Queries related to banners" > "$BASE_DIR/queries/bannerQueries.ts"
echo "// Consolidate all queries" > "$BASE_DIR/queries/index.ts"

# Log the completion message
echo "Queries folder and files created successfully!"


The commands `sanity manage` and `sanity docs` are additional helper commands in Sanity CLI that provide easy access to the project management dashboard and documentation, respectively.

### 1. **sanity manage**

   - Opens the Sanity project management dashboard in your web browser.
   - This dashboard allows you to manage settings, datasets, users, and other configurations for your Sanity project.
   - You can view your project ID, API tokens, CORS settings, and more, making it an essential tool for high-level project management tasks.
   - **Usage**:
     ```bash
     sanity manage
     ```
   - **Example Scenario**: If you need to add a new team member to the project, manage billing, or configure webhooks, you’d use `sanity manage` to access the online dashboard.

### 2. **sanity docs**

   - Opens the Sanity documentation in your default web browser.
   - Provides quick access to the official Sanity documentation, which is a comprehensive resource for learning about Sanity’s features, best practices, and examples.
   - This command is especially useful if you’re looking for guidance on specific configurations, API usage, or advanced customization options.
   - **Usage**:
     ```bash
     sanity docs
     ```
   - **Example Scenario**: If you're unsure about how to configure schema types or use GROQ (Sanity's query language), running `sanity docs` will take you directly to the documentation for further reading.

### Summary

- `sanity manage`: Opens the project management dashboard for your Sanity project in a web browser. It’s used for high-level configuration and project management.
- `sanity docs`: Opens the official Sanity documentation for easy access to guides, tutorials, and reference materials. Ideal for learning about new features and getting help with configurations.

Both of these commands are designed to make it easier to navigate Sanity's resources and tools by providing quick links to the online interfaces you need.

Sanity CLI is a command-line tool used to manage and interact with Sanity projects. Here are the main commands that are commonly used:

### 1. **sanity init**
   - Initializes a new Sanity project in the current directory.
   - You can use this command to create a new project, dataset, and basic structure.
   - **Example**:
     ```bash
     sanity init
     ```

### 2. **sanity start**
   - Starts the local development server for Sanity Studio.
   - This allows you to run and preview the studio locally.
   - **Example**:
     ```bash
     sanity start
     ```

### 3. **sanity deploy**
   - Deploys your Sanity Studio to Sanity’s hosting service.
   - This command makes your studio accessible online.
   - **Example**:
     ```bash
     sanity deploy
     ```

### 4. **sanity dataset**
   - Manages datasets in your project.
   - **Subcommands**:
     - `create`: Creates a new dataset.
       ```bash
       sanity dataset create <dataset-name>
       ```
     - `delete`: Deletes a specified dataset.
       ```bash
       sanity dataset delete <dataset-name>
       ```
     - `list`: Lists all datasets in the project.
       ```bash
       sanity dataset list
       ```

### 5. **sanity documents**
   - Manages the content documents in your dataset.
   - **Subcommands**:
     - `create`: Creates a new document in the dataset.
       ```bash
       sanity documents create <document-id>
       ```
     - `delete`: Deletes a document by its ID.
       ```bash
       sanity documents delete <document-id>
       ```
     - `import`: Imports documents from a local file.
       ```bash
       sanity documents import <file.ndjson> <dataset-name>
       ```
     - `export`: Exports documents to a file.
       ```bash
       sanity documents export <dataset-name> <output-file.ndjson>
       ```

### 6. **sanity hook**
   - Manages webhooks for your project.
   - **Subcommands**:
     - `create`: Creates a new webhook.
       ```bash
       sanity hook create
       ```
     - `delete`: Deletes a webhook by ID.
       ```bash
       sanity hook delete <hook-id>
       ```
     - `list`: Lists all webhooks in the project.
       ```bash
       sanity hook list
       ```

### 7. **sanity graphql**
   - Manages GraphQL schemas and endpoints.
   - **Subcommands**:
     - `deploy`: Deploys the current GraphQL schema to Sanity.
       ```bash
       sanity graphql deploy
       ```
     - `list`: Lists all GraphQL endpoints for the project.
       ```bash
       sanity graphql list
       ```

### 8. **sanity cors**
   - Manages allowed origins for Cross-Origin Resource Sharing (CORS).
   - **Subcommands**:
     - `add`: Adds a new origin to the allowed list.
       ```bash
       sanity cors add <origin>
       ```
     - `delete`: Removes an origin from the allowed list.
       ```bash
       sanity cors delete <origin>
       ```
     - `list`: Lists all allowed CORS origins.
       ```bash
       sanity cors list
       ```

### 9. **sanity project**
   - Manages project-level settings.
   - **Subcommands**:
     - `list`: Lists all available projects for the user.
       ```bash
       sanity project list
       ```
     - `create`: Creates a new Sanity project.
       ```bash
       sanity project create
       ```
     - `delete`: Deletes a specified project.
       ```bash
       sanity project delete <project-id>
       ```
     - `dataset`: Lists or manages datasets in a specific project.
       ```bash
       sanity project dataset list
       ```

### 10. **sanity login** / **sanity logout**
   - **login**: Logs into your Sanity account via the CLI.
   - **logout**: Logs out of your Sanity account.
   - **Examples**:
     ```bash
     sanity login
     sanity logout
     ```

### Summary

These commands cover the main functionalities needed to initialize, configure, and deploy a Sanity project, as well as manage content, datasets, and webhooks. You can always view more details on each command by adding the `--help` flag:

```bash
sanity <command> --help
```

This will provide additional options and subcommands for each command, helping you get more specific information about each feature in the Sanity CLI.