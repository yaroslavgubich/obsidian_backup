``` bash
# Add all changes to staging
git add .

# Commit the changes with a detailed message
git commit 

# Push the changes to the current branch
git push

#choose an option that suggests git "set upstream ..."
```


#push #template
example: 

``` bash
# Add all changes to staging
git add .

# Commit the changes with a detailed message
git commit -m "add feaures : 

- authentification drowpdown with clerk

"

# Push the changes to the current branch
git push

```

#terminal #command #folder with #document and #text

``` js
mkdir app/lib && echo "import { createClient } from "@sanity/client";

import imageUrlBuilder from "@sanity/image-url";

import dotenv from "dotenv";

dotenv.config();

  

export const client = createClient({

  projectId: "0opk9qht",

  dataset: "dataset",

  apiVersion: "2023-11-11",

  useCdn: true,

  token: process.env.SANITY_TOKEN,

});

  

// Create an image URL builder

const builder = imageUrlBuilder(client);

  

// Function to convert image references into URLs

export const urlFor = (source) => builder.image(source);" > app/lib/exampleDocument.js
```



#delete all #empty #files
```bash
find . -type f -empty -delete
```