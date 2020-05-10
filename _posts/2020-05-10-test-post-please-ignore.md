---
layout: post
title: "Test post please ignore"
---

Setting up a static site is easy, converting from Markdown to HTML is easy, but doing both together still yields a project with impressive complexity.

I've experienced:

* **Jekyll**: supported by GitHub pages natively, but otherwise annoying to set up (just install Ruby! Also that requires appending stuff to your .bashrc because Ruby Gems).
* **Hugo**: I actually got this working somewhat easily. After dealing with both Hugo and Jekyll I think I preferred Hugo slightly.
* **Gatsby**: Imagine wanting to make a static site from Markdown, finding a project that claims to do that and a couple other things, running `npm install gatsby`, and finding your `node_modules/` folder 1900 packages heavier. 1900!!
* **markdown-it**: what I probably should have used, given I just wanted a markdown repository.
* **GitHub**: In theory I could just create a repo with a bunch of markdown files and use GitHub's built-in code browser to sift through it all. Would that be _negative_ nerd cred, though?

In the end I stuck with Jekyll. At least GitHub takes care of the build chain here, and there are a few themes to choose from when I realize my DIY barebones CSS is awful. Plus look at this fancy syntax highlighting:

```javascript
const woot = () => {
    console.log(`This is a test`);
    return 4;
}
```

This setup is simple enough to mark down as done.
