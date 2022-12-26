# Dynamic Blog System with Next.js

Using the file system and markdown files to create a simple blog system.

## Overview

### Versions

- **Next.js:** 12.0.4+
- **Ubuntu:** 22.04 LTS

## Setup

### Installing Pre-requisites

To acomplish this, we will need to install the following:

- gray-matter
- react-markdown

```bash
npm install gray-matter react-markdown
```

### Listin all blog posts

To list all blog posts, we will need to create a function that will read all the files in the `data/posts` directory and return an array of objects with the metadata and slug of each post.

```ts
import fs, { readFileSync } from "fs"; // used for reading files
import path from "path"; // used for joining paths
import matter from "gray-matter"; // used for parsing the metadata

// pass 'posts' as a prop to the component
function AllPosts({ posts }: any) {
  return (
    <div>
      {posts.map((post: any, index: any) => (
        <Post key={index} post={post} />
      ))}
    </div>
  );
}

// get all the posts
export async function getStaticProps() {
  const postsDirectory = path.join(process.cwd(), "data/posts"); // specify the directory where the posts are stored
  const files = fs.readdirSync(postsDirectory); // read all the files in the directory

  const posts = files.map((filename) => {
    const slug = filename.replace(".md", ""); // 'slug' is the name of the file, used in the url

    const markdownWithMeta = readFileSync(
      path.join(postsDirectory, filename),
      "utf-8"
    );

    const { data: meta, content } = matter(markdownWithMeta); // use gray-matter to parse the metadata and content

    return {
      slug,
      meta,
      content,
    };
  });

  return {
    props: {
      posts: posts,
    },
  };
}
```

### Displaying a single blog post

To display a single blog post, we will need to create a function that will read the file in the `data/posts` directory and return an object with the metadata and content of the post.

```ts
import fs from "fs"; // used for reading files
import path from "path"; // used for joining paths
import matter from "gray-matter"; // used for parsing the metadata
import ReactMarkdown from "react-markdown"; // used for rendering markdown

// pass 'post' as a prop to the component
function Post({ post }: any) {
  return (
    <div>
      <h1>{post.meta.title}</h1>
      <ReactMarkdown>{post.content}</ReactMarkdown>
    </div>
  );
}

// get the slug from the url
export async function getStaticPaths() {
  const file = fs.readdirSync(path.join(process.cwd(), "data/posts")); // read all the files in the directory

  return {
    paths: file.map((filename) => ({
      params: {
        slug: filename.replace(".md", ""), // 'slug' is the name of the file, used in the url
      },
    })),
    fallback: false,
  };
}

// get the post from the slug
export async function getStaticProps({ params: { slug } }: any) {
  const markdownWithMeta = fs.readFileSync(
    path.join(process.cwd(), "data/posts", slug + ".md"),
    "utf-8"
  );
  const { data: meta, content } = matter(markdownWithMeta); // use gray-matter to parse the metadata and content

  const post = {
    slug,
    meta,
    content,
  };

  return {
    props: {
      post: post,
    },
  };
}
```
