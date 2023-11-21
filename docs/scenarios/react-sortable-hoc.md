---
id: react-sortable-hoc
title: React Sortable HOC
sidebar_label: React Sortable HOC
slug: /react-sortable-hoc/
---

The example below integrates the library with [React Sortable HOC](https://github.com/clauderic/react-sortable-hoc).
Drag any of the items around - dropping it outputs the information in the console.

The example is contributed by [mitchellwarr](https://github.com/mitchellwarr).

```jsx live include-data import=react-sortable-hoc
import * as ReactSortableHOC from 'react-sortable-hoc'
import { Virtuoso } from 'react-virtuoso'
import { generateUsers } from './data'
import React from 'react'

const ItemContainerSortable = ReactSortableHOC.sortableElement((props) => <div {...props} />)
const ListContainerSortable = ReactSortableHOC.sortableContainer(({ listRef, ...props }) => <div ref={listRef} {...props} />)

const components = {
  List: React.forwardRef((props, ref) => {
    return <ListContainerSortable {...props} listRef={ref} onSortEnd={(...args) => console.log(args)} />
  }),
  Item: (props) => {
    const { ['data-index']: index } = props
    return <ItemContainerSortable index={index} {...props} />
  },
}

export default function App() {
  return (
    <Virtuoso
      style={{ height: 400 }}
      data={generateUsers(100)}
      components={components}
      itemContent={(index, user) => {
        return (
          <div style={{ backgroundColor: user.bgColor, padding: '1rem 0.5rem' }}>
            <h4>
              {user.index}. {user.name}
            </h4>
            <div style={{ marginTop: '1rem' }}>{user.description}</div>
          </div>
        )
      }}
    />
  )
}
```
