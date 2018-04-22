# NgxBearbones

A project to create bare-bones (get it?) Angular widgets ready to be used with any CSS framework. (Bootstrap, Material, SemanticUI, etc.)

**Note**: The ngx-bearbones package currently only contains two completed widgets, a drag-and-drop directive and a sortable directive. I'm working as fast as I can to add more!

## Table of contents
1. [Bearbones Manifesto](#manifesto)
2. [Installation instructions](#installation-instructions)
3. [Documentation](#documentation)
3. [Troubleshooting](#troubleshooting)
4. [Contributing](#contribution)

## Bearbones Manifesto

There are dozens of Angular widget libraries for multiple CSS frameworks, but there are very few entirely unthemed, functional widgets that allow you to easily implement your own custom styles or test different CSS frameworks without extensively rewriting your components for them.

Enter **Bearbones**, which gives you complete widgets that are not integrated with any CSS framework, but can work with any of them.

* Easily create your own classes for widget components, without having to override existing styles.
* Switch between CSS frameworks as easily as switching class names on a `<div>`.
* Test components without flashy styles getting in the way, while still being fully functional.
* Apply **Bearbones** directives to nearly any HTML element, instead of being locked into specific templates.

## Installation instructions

Install `ngx-bearbones` from `npm`:
```bash
npm install ngx-bearbones --save
```

Import the Bearbones module:
```
import { BearbonesModule } from 'ngx-bearbones';

@NgModule({
  ...
  imports: [ BearbonesModule, ... ]
  ...
})
```

## Documentation

Use ngx-bearbones widgets in your components.

### Sortable

A sortable widget that emits an event `orderChanged` whenever an item in a list of items (usually an array) has been dragged to a new position. The event object consists of just two fields, both of which are numbers:

```typescript
{
    draggedItem, // The index of the item you are dragging
    newPosition  // The item's new position - i.e., the drop target's index
}
```

**Note**: The "bbsortable" directive does not reposition the elements for you, which is by design. In order to accomplish maximum compatibility with any CSS framework and development style, it is up to you decide what to do with the positioning information contained in the event. See an example of reordering items in an array that is accessed with `*ngFor` from a template:

#### Example Template

```HTML
<ul bbsortable="mysortable" (orderChanged)="orderChanged($event)">
    <li *ngFor="let item of myItems">{{item.name}}</li>
</ul>
```

#### Example Component

```typescript
myItems = [
    { name: 'Item 1' },
    { name: 'Item 2' },
    { name: 'Item 3' }
];

orderChanged(event: any) {
    const { draggedItem, newPosition } = event;
    this.myItems.splice(newPosition, 0, this.myItems.splice(draggedItem, 1)[0]);
}
```

Example using custom classes:

#### Template
```HTML
<ul bbsortable="mysortable" (orderChanged)="orderChanged($event)" [bboptions]="myOptions">
    <li *ngFor="let item of myItems">{{item.name}}</li>
</ul>
```

#### Component

```typescript
myItems = [
    { name: 'Item 1' },
    { name: 'Item 2' },
    { name: 'Item 3' }
];

myOptions = {
    restingClass: 'dropzone',
    hoverClass: 'dropzone-hover',
    holdingClass: 'dropper-holding'
};

orderChanged(event: any) {
    const { draggedItem, newPosition } = event;
    this.myItems.splice(newPosition, 0, this.myItems.splice(draggedItem, 1)[0]);
}
```

### Drag and drop

The drag-and-drop component consists of two directives, a dropzone target and a dropper. Both target and dropper can be any HTML element; I've intentionally made it as unrestrictive as possible, but that means it's up to you to make sure you haven't accidentally created a `<li>` dropper and a `<div>` drop target on the same page.

#### Example

```HTML
<ul>
    <li bbdropzone bbdropzoneClass="dropzone" bbdropzoneHoverClass="dropzone-hover">
        <div bbdropper bbdropperClass="dropper" bbholdingClass="dropper-holding">
            Styled dropper
        </div>
    </li>
    <li bbdropzone bbdropzoneClass="dropzone" bbdropzoneHoverClass="dropzone-hover"></li>
    <li bbdropzone bbdropzoneClass="dropzone" bbdropzoneHoverClass="dropzone-hover"></li>
</ul>
```

## Troubleshooting

Under construction! Please come back later...

## Contributing

Also under construction, but feel free to create pull requests!
