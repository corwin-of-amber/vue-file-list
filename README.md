# vue-file-list

A small collection of Vue components for creating customizable file lists.
Supports common operations such as dragging files to reorder or move them,
and renaming files by editing directly in the list.

The data model is a dead-simple list of objects with a `name` string property.
Folders have an additional `files` property which should be an array of
nexted objects with the same structure.

```html
<file-view :files="[{name: 'folder',
                     files: [{name: 'file1', name: 'file2'}]},
                    {name: 'file3'}]"/>
```