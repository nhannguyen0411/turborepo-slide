---
# try also 'default' to start simple
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
# apply any windi css classes to the current slide
class: 'text-center text-white bg-black'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# persist drawings in exports and build
drawings:
  persist: false
# use UnoCSS (experimental)
css: unocss
---

<div class="flex relative justify-center py-12">
  <div id='turbo-img'></div>
  <div id='turbo-bg'></div>
  <img class='relative z-10' src='https://turbo.build/images/docs/repo/repo-hero-logo-dark.svg' />
</div>

# Welcome to Turborepo

<div class='max-w-sm mx-auto text-gray-400'>A high-performance build system for JavaScript and TypeScript codebases</div>

<div class="pt-12 text-gray-600">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

<style>
  #turbo-img {
    border-radius: 9999px;
    width: 128px;
    height: 128px;
    position: absolute;
    top: 20%;
    left: 42.5%;
    filter: blur(32px);
    background: conic-gradient(
      from 180deg at 50% 50%,
      #2a8af6 0deg,
      #a853ba 180deg,
      #e92a67 1turn
    );
  }
  #turbo-bg {
    opacity: 0.2;
    border-radius: 9999px;
    width: 500px;
    height: 500px;
    position: absolute;
    top: -45%;
    left: 20%;
    mix-blend-mode: normal;
    filter: blur(75px);
    will-change: filter;
    background: conic-gradient(
      from 180deg at 50% 50%,
      #2a8af6 0deg,
      #a853ba 180deg,
      #e92a67 1turn
    );
  }
</style>

---
class: 'text-white bg-black'
css: unocss
---

# **Why is Turborepo?**

- **Incremental builds** - Building once is painful enough, Turborepo will remember what you've built and skip the stuff that's already been computed.

- **Content-aware hashing** - Turborepo looks at the contents of your files, not timestamps to figure out what needs to be built.

- **Parallel execution** - Execute builds using every core at maximum parallelism without wasting idle CPUs.

- **Remote Caching** - Share a remote build cache with your teammates and CI/CD for even faster builds.

<br>
<br>

Read more about [Why Turborepo?](https://turbo.build/repo)

<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/guide/syntax#embedded-styles
-->

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(180deg, #4EC5D4 100%, #146b8c 10%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---
class: 'bg-black text-white'
css: unocss
---

# **Caching tasks**

- Every JavaScript or TypeScript codebase will need to run package.json scripts, like `build`, `test` and `lint`. In Turborepo, we call these **tasks**.

- Turborepo can cache the results and logs of your tasks - leading to enormous speedups for slow tasks.

<v-click>

```ts
@koffi/sign:build: build/assets/vendor-NRf-pVlz.js                             162.44 kB │ gzip:  52.89 kB
@koffi/sign:build: build/assets/index-GzbzsB0-.js                              162.49 kB │ gzip:  49.38 kB
@koffi/sign:build: build/assets/chart.js-Y8bwA105.js                           164.93 kB │ gzip:  57.50 kB
@koffi/sign:build: build/assets/@koffi/picker-o26WmqQi.js                      291.87 kB │ gzip:  71.94 kB
@koffi/sign:build: build/assets/react-pdf-FkfKBID5.js                          337.23 kB │ gzip:  94.18 kB
@koffi/sign:build: build/assets/@koffi/pdf-La5ekmQP.js                         471.69 kB │ gzip: 129.52 kB
@koffi/sign:build: ✓ built in 6.70s

 Tasks:    72 successful, 72 total
Cached:    71 cached, 72 total
  Time:    7.727s 

```
</v-click>


<style>
p code {
  background-color: #6c6a6a;
}
.highlighted {
  background-color: #f8f8f8;
}
</style>

---
class: 'bg-black text-white'
css: unocss
---

# **Missing the cache**

<div grid="~ cols-2 gap-4">
<div>

Each task in your codebase has **inputs** and **outputs**.

- A build task might have source files as inputs and outputs logs to `stderr` and `stdout` as well as bundled files.

- A `lint` or `test` task might have source files as inputs and outputs logs to `stdout` and `stderr`.

Let's say you run a `build` task with Turborepo using `turbo run build`:

</div>
<div>

<img src='https://turbo.build/_next/image?url=%2F_next%2Fstatic%2Fmedia%2Fcache-miss.21d45e92.png&w=3840&q=75&dpl=dpl_9S8Sn3R13VwbGE6foKG3PqsBY14T'/>

</div>
</div>

<div v-click class='px-5 py-0.5 rounded mt-5 bg-blue'>

Turborepo takes a lot of information into account when creating the hash: the dependency graph, tasks it depends on, source files, environment variables, and more!

</div>

<style>
p code {
  background-color: #6c6a6a;
}
</style>

---
layout: center
class: 'bg-black text-white'
css: unocss
---

# **Hitting the cache**

<div class='flex justify-center mt-5'>

<img src='https://turbo.build/_next/image?url=%2F_next%2Fstatic%2Fmedia%2Fcache-hit.3bac1eb9.png&w=3840&q=75&dpl=dpl_9S8Sn3R13VwbGE6foKG3PqsBY14T' />

</div>

<div v-click class='px-5 py-0.5 mt-5 rounded bg-blue'>

Restoring files and logs from the cache happens near-instantaneously. This can reduce your build times from minutes or hours down to seconds or milliseconds. Although specific results will vary depending on the shape and granularity of your codebase's dependency graph, most teams find that they can reduce their overall monthly build time by around 40-85% with Turborepo's caching.

</div>

<style>
img {
  width: 700px;
  height: 250px;
}
</style>

---
class: 'bg-black text-white'
css: unocss
---

# **Remote Caching**

<div>

Turborepo's task cache can save a lot of time by never doing the same work twice.

But there's an issue - the **cache is local to your machine**. When you're working with a CI, this can result in a lot of duplicated work:

</div>

<img src='https://turbo.build/_next/image?url=%2F_next%2Fstatic%2Fmedia%2Flocal-caching.d097807f.png&w=3840&q=75&dpl=dpl_9S8Sn3R13VwbGE6foKG3PqsBY14T' />

<style>
img {
  height: 320px;
  width: 850px;
}
</style>

---
class: 'bg-black text-white space-y-5'
css: unocss
---

# **A single, shared cache**

<div grid='~ cols-2 gap-4'>
<div>

  What if you could share a single Turborepo cache across your entire team (and even your CI)?

  By working with providers like Vercel, Turborepo can securely communicate with a remote cache - a cloud server that stores the results of your tasks.

  This can save enormous amounts of time by **preventing duplicated work across your entire organization**.
</div>

<div class='mt-5 flex justify-center'>

  <img src='https://turbo.build/_next/image?url=%2F_next%2Fstatic%2Fmedia%2Fremote-caching.5c826549.png&w=3840&q=75&dpl=dpl_9S8Sn3R13VwbGE6foKG3PqsBY14T' />

</div>

</div>


<div v-click class='px-5 mt-5 py-3 bg-orange-200 rounded text-orange-700'>
  Remote Caching is a powerful feature of Turborepo, but with great power comes great responsibility. Make sure you are caching correctly first and double check handling of environment variables. Please also remember Turborepo treats logs as artifacts, so be aware of what you are printing to the console.
</div>
