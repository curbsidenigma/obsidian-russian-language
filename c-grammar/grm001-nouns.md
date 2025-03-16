---
tags:
  - grammar
  - nouns
  - index
aliases:
  - Nouns
parent: "[[c-grammar|Grammar]]"
---
# Nouns
---
```dataviewjs
// Get property parent from path
const getParent = (path) => String(dv.page(path).file.frontmatter.parent)
// Get property aliases from path
const getAlias = (path) => String(dv.page(path).file.aliases).slice(1,-1)

// Set current file
const current = dv.current().file
// Set folder string named after the current file
const folder = `"${String(current.path).slice(0,-3)}"`
// Set array of file paths whose parent is the current file
const paths = dv.pagePaths(folder).where(
	path => getParent(path) == `[[${current.name}|${getAlias(current.path)}]]`
)

// Set index list class name
dv.container.className += ' index'
// Render list of links
dv.list(
	paths.sort(path => dv.page(path).file.name)
	.map(
		path => dv.fileLink(path, false, getAlias(path))
	)
)
```