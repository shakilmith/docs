## Programmatically Create MDX pages in gatsbyjs


1. Install the following dependencies in your gatsby project
   
```
npm install gatsby-plugin-mdx gatsby-source-filesystem @mdx-js/react
```

2. Create a folder in top level directory like this: content/posts or content only.
3. In content folder add few mdx posts.
4. Update gatsby-config.js file like this:

```
plugins: [
    //other plugins
    "gatsby-plugin-mdx",
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `content`,
        path: `${__dirname}/content`,
      }
    }
]
```
Note: in content folder - top level directory (yes it can be relative to src folder) or content/posts folder, your mdx posts will reside.

5. Create gatsby-node.js file in top level directory. it helps to generate mdx pages (even any type of pages) programmatically.

gatsby-node.js file (add this minimal code for creating pages for each mdx posts)

```
const path = require("path")

//post template path
const postTemplate = path.resolve(`./src/templates/post.js`)

exports.createPages = async ({ graphql, actions, reporter }) => {
  const { createPage } = actions

  const result = await graphql(`
    query {
      allMdx {
        nodes {
          id
          frontmatter {
            title
            slug
          }
          internal {
            contentFilePath
          }
        }
      }
    }
  `)

  if (result.errors) {
    reporter.panicOnBuild('Error loading MDX result', result.errors)
  }

  // Create blog post pages.
  const posts = result.data.allMdx.nodes

  // you'll call `createPage` for each result
  posts.forEach(node => {
    const slug = node.frontmatter.slug
    createPage({
      path: `/${slug}`,
      component: `${postTemplate}?__contentFilePath=${node.internal.contentFilePath}`,
      context: { 
        id: node.id 
    },
    })
  })
}
```

6. Create a post.js template file in src/templates folder
   
```
import React from "react"
import { graphql } from "gatsby"
import { MDXProvider } from "@mdx-js/react"
import { Link } from "gatsby"

const shortcodes = { Link } // Provide common components here

export default function PageTemplate({ data, children }) {
  return (
    <>
      <h1>{data.mdx.frontmatter.title}</h1>
      <MDXProvider components={shortcodes}>
        {children}
      </MDXProvider>
    </>
  )
}

//graphql query
export const query = graphql`
  query($id: String!) {
    mdx(id: { eq: $id }) {
      frontmatter {
        title
      }
    }
  }
`
```

7. In order to render list of mdx pages

Create a list.js file in the src/templates folder

```
import * as React from "react"
import { graphql, Link } from "gatsby"

const BlogListTemplate = ({ data }) => {
  const posts = data.allMdx.nodes

  return (
    <main>
      <h1>Blog</h1>

      <ul>
        {posts.map(post => (
          <li key={post.id}>
            <Link to={post.frontmatter.slug}>
              <h2>{post.frontmatter.title}</h2>
            </Link>
            <p>{post.frontmatter.date}</p>
          </li>
        ))}
      </ul>
    </main>
  )
}

export default BlogListTemplate

export const query = graphql`
  query {
    allMdx(sort: { frontmatter: { date: DESC } }) {
      nodes {
        id
        frontmatter {
          title
          date(formatString: "MMMM DD, YYYY")
          slug
        }
      }
    }
  }
`
```

8. Now make this component as a page using createPage api

gatsby-node.js

```
createPage({
  path: "/blog",
  component: require.resolve("./src/templates/blog-list.js"),
})
```

Note: you can render many things like title, slug etc. using context api.

9. Create Pages based on category
You can also create pages based on category. First of of add category in your mdx posts. Like,

```
---
title: "My First Post"
slug: "/my-first-post"
category: "javascript"
---

Post content here...
```

then modify your graphql query to include category field.

```
const result = await graphql(`
  query {
    allMdx {
      nodes {
        id
        frontmatter {
          title
          slug
          category
        }
        internal {
          contentFilePath
        }
      }
    }
  }
`)
```

Now extract unique categories after getting all posts.

**Getting Unique category** (Using new Set() method)
```
const posts = result.data.allMdx.nodes

// collect categories (all unique categories)
const categories = new Set()

//query category and add category to the "categories" if there is a category.
posts.forEach(post => {
  if (post.frontmatter.category) {
    categories.add(post.frontmatter.category)
  }
})
```

**Create category template**

You can import the categoryTemplate in top of the file, for ease.
```
const categoryTemplate = path.resolve(`./src/templates/category.js`)
```

**Now create category pages** (it list the posts based on category.)

Same as, how you build mdx pages programmatically.

```
categories.forEach(category => {
  createPage({
    path: `/category/${category}`,
    component: categoryTemplate,
    context: {
      category: category
    }
  })
})
```

**category.js file in templates folder**

```
import React from "react"
import { graphql } from "gatsby"

export default function CategoryPage({ data, pageContext }) {
  const posts = data.allMdx.nodes

  return (
    <div>
      <h1>Category: {pageContext.category}</h1>

      {posts.map(post => (
        <div key={post.id}>
          <a href={post.frontmatter.slug}>
            {post.frontmatter.title}
          </a>
        </div>
      ))}
    </div>
  )
}

export const query = graphql`
  query($category: String) {
    allMdx(
      filter: { frontmatter: { category: { eq: $category } } }
    ) {
      nodes {
        id
        frontmatter {
          title
          slug
        }
      }
    }
  }
`
```

9. Create Pages based on tags 

mdx post look like:

```
title: "My First Post"
slug: "/my-first-post"
category: "gatsby"
tags: ["gatsby", "react", "blog"]
```

**Collect unique tags**

```
const tags = new Set()

posts.forEach(post => {
  if (post.frontmatter.tags) {
    post.frontmatter.tags.forEach(tag => {
      tags.add(tag)
    })
  }
})
```

**now create pages based on tags**
```
const tagTemplate = path.resolve(`./src/templates/tag-template.js`)

tags.forEach(tag => {
  createPage({
    path: `/tags/${tag}`,
    component: tagTemplate,
    context: {
      tag: tag,
    },
  })
})
```

Note, you have to create a tag template page.

```
```